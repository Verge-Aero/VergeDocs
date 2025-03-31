---
hidden: true
---

# VRSP

The **V**erge **R**obotics **S**treaming **P**rotocol is a real-time network protocol that is designed to enable third-party applications to display the active state of a Verge Design Studio session.

The protocol supports any&#x20;

All VRSP packets start with a standard header:

`Packet Identifier:` \[**string**] A string starting with "VRSP\_" followed by a packet identifier

`Version:` \[**uint8**] **I**ndicates the protocol's version \[Currently always 1]

`Instance ID:` \[**uint32**] An unsigned integer that identifies a specific swarm configuration

***

## Definition Packet - `"VRSP_DEF"`

Definition packets are responsible for providing static information about an active swarm. When a new definition is created or its content is changed, the packet's instance ID is regenerated as a pseudo-random 32-bit unsigned integer. Before any data packets are parsed, at least one definition packet with a matching instance ID must be received.&#x20;

Definition packets are sent out at a reduced rate (Default: 1 Hz) as their contents are not expected to change often.

A definition packet consists of the following information:

`Device Count:` \[**uint32**] The number of expected devices in the stream

`Root Latitude:` \[**double**] The exact latitude location that  maps to \[0.0.0] in local space

`Root Longitude:` \[**double**] The exact longitude location that maps to \[0,0,0] in local space

`Root Altitude:` \[**double**] The exact altitude location that maps to \[0,0,0] in local space

```csharp
int DeviceCount;
double RootLatitude;
double RootLongitude;
double RootAltitude;
```

After the definition packet header, device definitions are serialized along with a list of device IDs that are represented by each definition. An embedded JSON string is used to serialize device info and payload information.

For each unique definition, the following is written:

`Definition Device Count:` \[**uint32**] The number of devices that use this device definition

`Definition String Length:` \[uint32] The length of the definition JSON payload

`Definition String:` \[UTF-8 String] A JSON-formatted string that contains device and payload definitions

`Device IDs:` \[uint16 Array] An array of device IDs that use this definition. Array length matches _Definition Device Count_

The JSON-formatted definition contains information about the device as well as information about attached payloads.

### Device Definition

A single device definition entry contains three fields:

`Definition ID:` \[Integer] A unique 0-based index that can be used to differentiate between definition table entries

`Model Name:` \[String] A human-readable name that indicates the drone or device that is being described

`Payload Definitions:` \[Object Array] A list of payload definition objects that describe the attached elements based on their type as well as their mounting methodology. These definitions are important for resolving data packets and understanding how to render the final result.

### Payload Definition

```yaml
{
  "DefinitionID": 1,
  "DeviceModel": "X7",
  "LightLumens": "900",
  "PayloadDefinitions": [
    {
      "DefType": "Pyro",
      "MountDef": "Static",
      "Cues": [
        {
          "ID": 1,
          "VDL": "Silver Waterfall 10s",
          "MountDirection": {
            "w":0,
            "x":0,
            "y":0,
            "z":1
          }
        },
        {
          "ID": 4,
          "VDL": "red comet three times",
          "MountDirection": {
            "w":0,
            "x":1,
            "y":0,
            "z":0
          }
        }
      ]
    },
    {
      "DefType": "Laser",
      "MountType": "2DOF",
      "Color": {
        "r":255,
        "g":0,
        "b":0
      }
    }
  ]
}
```

Payload definitions must contain a "DefType" and a "MountType". Other fields differ depending on the "DefType"

#### Standard Definition Fields

`MountType:` Describes the type of mount in use. Currently supports "Static" and "2DOF"/"3DOF" (typically a gimbal).

#### Light Payload Definition - "Light"

This is a description of a light source that _is not_ the same as the one typically built-in as part of a drone light show drone. Characteristics are defined in the payload definition field of the definition packet. This payload type also supports spotlights.

`LightLumens:` Indicates the maximum intensity of the light source in lumens.

`Color [Optional]:` If present, this object describes a fixed light color. Payload data is then expected to serialize a single intensity value rather than RGB values.

`LightType [Optional]:` Can be included to describe the type of the light source. Writing "Spotlight" will describe the payload as a targetable spotlight rather than the default point light.

If the light is a "Spotlight" then the following fields are supported:

`SpotAngle:` The angle of the spot light's cone in degrees.

#### Pyro Payload Definition - "Pyro"

This is a description of attached pyro products. This also includes each cue's mounting direction.

`Cues:` An array of cues that represent the available pyro payloads. When triggered in a data packet, these descriptions provide all necessary information for rendering the pyro product.

`ID:` The 1-based Cue ID for the product. This is used to identify which product is being fired.

`VDL:` This field provides the definition of the pyro product [Finale3D's VDL](https://finale3d.com/documentation/vdl-effect-glossary/).

`MountDirection:` A quaternion that provides a rotation (from forward) of the product as it is mounted on the platform.

#### Laser Payload Definition - "Laser"

A description of an attached laser. Functionally similar to spotlights, but with a very small spot angle.

`Color [Optional]:` If present, this object describes a fixed light color. Payload data is then expected to serialize a single intensity value rather than RGB values.

***

## Data Packet - `"VRSP_DATA"`

Data packets contain serialized swarm state data. This includes position and all data describing the current state of attached payloads. Payload data is serialized according to options described in the payload definition fields of the definition packet.

```csharp
//Required
float X;
float Y;
float Z;
byte OptionFlags;
//Optional
color32 LightColor; //0x1
half Heading; //0x2
half4 Orientation; //0x4 w,x,y,z
```

### Position \[Required]

Local coordinates are encoded using a left-handed coordinate system, where y is up.

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

| Variable | Local Direction | Global Direction |
| -------- | --------------- | ---------------- |
| X        | Right           | East             |
| Y        | Up              | Up               |
| Z        | Forward         | North            |

### Optional Data

Additional device characteristics can be included here based on the value of the option flags:

#### Light Color \[Optional] (0x1) :&#x20;

An RGB, 24-bit value that indicates the current color of the device's LED payload.

#### Heading \[Optional] (0x2):&#x20;

An 16-bit floating point value that indicates which way the device is pointing.

#### Orientation \[Optional] (0x4): &#x20;

Represented by a half-precision quaternion, this provides a full description of the device's rotation.



### Payload Mounting Devices

***

### Payload Options

Payload options are serialized raw data. Some contents can be inferred from the details provided in the definition packets.

There are currently payload data fields for the following types:

### Light

#### RGB Color - If RGB Source

`Red Channel:` \[uint8] A value between 0-255 that indicates the intensity of the red light source

`Green Channel:` \[uint8] A value between 0-255 that indicates the intensity of the green light source

`Blue Channel:` \[uint8] A value between 0-255 that indicates the intensity of the blue light source

#### Intensity - If fixed color

`Intensity:` \[uint8] A value between 0-255 that indicates the intensity of the light source

### Pyro

`Cue ID:` \[uint8] Using this ID and referencing the associated payload definition will allow the exact attached product to be resolved.

`Time Since Trigger:` \[ushort] The time, in milliseconds, since the pyro fired. Pyro descriptors are only expected to be present for the duration of a pyro effect. This is useful for synchronization purposes.

### Laser

#### RGB Color - If RGB Source

`Red Channel:` \[uint8] A value between 0-255 that indicates the intensity of the red

`Green Channel:` \[uint8] A value between 0-255 that indicates the intensity of the green light source

`Blue Channel:` \[uint8] A value between 0-255 that indicates the intensity of the blue light source

#### Intensity - If fixed color

`Intensity:` \[uint8] A value between 0-255 that indicates the intensity of the light source

***

### Payload Locomotion:&#x20;

If a payload is affixed to a gimbal or other manipulation device, then it is serialized after the other payload data. If the platform itself has a yaw or orientation definition, that must be accounted for on the payload's final transform solution.

#### Static

The module is hard-mounted to the platform. The payload's orientation or direction is described in the definition packet. No data is serialized here.

#### 2-DOF / 3-DOF

Either of these options embed a half4 quaternion. Rotation limits are enforced by the sending application.
