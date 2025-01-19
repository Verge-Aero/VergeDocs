---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# VVIZ Format

## The VVIZ Format

VVIZ stands for **\[V]**&#x65;rge **\[Vi]**&#x73;ual&#x69;**\[z]**&#x61;tion Format. This format has been adopted by multiple software vendors as an interchange format for drone shows. The format has support for exporting drone position, colors, pyro payloads and more.

VVIZ files are human readable, JSON-formatted strings. They are not intended to output flight-ready path data are also unsuitable for external validation. The file is meant for providing data for visualization only.

***

### VVIZ Header Data

A set of entries can be found at the start of the file that provide reference values on how other data in the file should be interpreted.

```json
  "version": "1.0",
  "performanceName": "VVIZTest",
  "coordinateFrame": "ogl",
  "globalReferenceFrame": {
    "lat": 39.905963,
    "lon": -75.166393,
    "alt": 0.0
  },
  "defaultPositionRate": 3.0,
  "defaultColorRate": 16.0,
  "timeOffsetSecs": 0.0,
```

`"version"`: Indicates the file type revision represented by this file. It will only be incremented when any backwards compatibility-breaking changes are made.

`"performanceName"`: Provides a field for naming the performance. Largely useful for identification purposes.

`"coordinateFrame"`: Indicates what coordinate system is used to convert from xyz to real-world coordinates. "ogl" refers to X = right, Y = up, and Z = forward

`"globalReferenceFrame"`: This object contains a latitude, longitude, and altitude "root" that corresponds to the 0,0,0 coordinate of the local space that all drones occupy.

`"defaultPositionRate"`: If a delta time is not listed for a traversal frame, then assume that the time step is:

$$
dt = \dfrac{1}{defaultPositionRate}s
$$

`"defaultColorRate"`: Unlike position coordinates (which uses deltas in seconds), payload color data deltas are measured in frames. Frames are always represented as a fixed delta time of:

$$
dt = \dfrac{1}{defaultColorRate}s
$$

`"timeOffsetSecs"`: This indicates that an offset should be applied to all color and positional data contained in the file. This is useful for manually synchronizing content to fit timelines in third-party design or visualization applications.

***

### Event Tags

Event tags are markers that indicate the start of some discrete event. They are a useful way to understand the intent of designers when synchronizing with external elements, such as audio, video screens, or ground pyro.

```json

  "eventTags": [
    {
      "time": 20.0,
      "tagType": "EffectStart",
      "tagID": "Zombie",
      "color": {
        "r": 1.0,
        "g": 1.0,
        "b": 1.0
      }
    },
    {
      "time": 30.05,
      "tagType": "SongStart",
      "tagID": "Thriller",
      "color": {
        "r": 0.3378955,
        "g": 1.0,
        "b": 0.0
      }
    },
    {
      "time": 30.05,
      "tagType": "PyroStart",
      "tagID": "Mines",
      "color": {
        "r": 1.0,
        "g": 0,
        "b": 0.0
      }
    }
  ],
```

`"time"`: Indicates the time in seconds (since start) that this event occurs

`"tagType"`: Required field that&#x20;

`"tagID"`: An optional field that helps to differentiate two or more tags with the same type

`"color"`: An optional field that allows tags to be colored for visualization purposes

***

## Performances

The "performances" field contains an ordered list of objects that describe all movements and payload actions that occur in the show.

A single performance contains two entries, an agent description, and a payload description. _Agent_ is a generic term for an autonomous vehicle in this case. The agent description contains a definition of its starting, or home, location as well as arbitrary information about the agent that may be useful in third-party applications.

```json
"agentDescription": {
        "homeX": -6.85800028,
        "homeY": 0.05000041,
        "homeZ": -6.858,
        "homeH": 180,
        "airframe": "Verge_X1",
        "agentTraversal": [
          {
            "dx": 0.0,
            "dy": 0.0666669756,
            "dz": 0.0,
            "dh": 0.0,
            "dt": 14.666667
          },
          {
            "dx": 0.0,
            "dy": 3.93333149,
            "dz": 0.0,
            "dh": 0.0,
            "dt": 4.0
          },
          ...
        ]
      }
```

### Home `"homeX"`, `"homeY"`, `"homeZ"`, `"homeH"`

The agent description contains a local-space XYZ position that indicates its starting location. Additionally, it includes a home heading angle (in degrees) which indicates its initial heading. Use this as the starting position when initializing agent positions and performing the delta steps in the following section.

### Drone Position and Heading : `"agentTraversal"`

Drone coordinates are delta compressed. This means that each step contains data representing the change in position, heading, and time since the previous step rather than providing absolute values. To reconstruct drone coordinates, initialize its state at its "home" values and then add the delta values  (`dx`, `dy`, `dz`,`dh`) to create a new frame. Step the time (`dt`) in the next frame and then add the new deltas to the coordinates from previous frame. Continue this process until all frames have been consumed.

{% hint style="info" %}
Heading can be modified via [Yaw Control](advanced-topics/yaw-control.md) in the Verge Design Studio
{% endhint %}

### Payloads

The behavior of payloads, any device being carried by an agent, is described via the `"payloadDescription"`  object. There are currently two payload types supported, `"Light"` and `"Pyro"`.

### Light Payloads

If the `"type"` is labeled as `"Light"` then it is a pyro trigger payload.

```json
"payloadDescription": [
        {
          "type": "Light",
          "lumens": 900.0,
          "colorType": "RGBW",
          "sourceType": "Dome",
          "payloadActions": [
            {
              "r": 0,
              "g": 0,
              "b": 0
            },
            {
              "r": 255,
              "g": 255,
              "b": 255,
              "frames": 583
            }
          ]
        }
      ]
```

The payload description may contain optional fields describing the light characteristics. This offloads the need to know about a specific drone's characteristics to the designer. These fields include:

`"lumens"` : The light's max output in lumens

`"colorType"`: The light die sources. This is typically RGB or RGBW.

`"sourceType"`: Allows the light's shape to be defined. Standard diffusers are "dome", but other types such as "spotlight" could be expected here

#### Light Payload Playback

The object `"payloadActions"`  contains an array of light data _chunks_. A red, green, and blue channel with values between 0-255 represent a standard 24-bit color. If a step contains a `"frames"` variable, then it can be assumed that this color is held for a length of frames equal to its value. The length of a frame is located in the header under `"defaultColorRate"`. If no such entry exists, then it represents a single frame.&#x20;

### Pyro Payloads

If the `"type"` is labeled as `"Pyro"` then it is a pyro trigger payload.

<pre class="language-json"><code class="lang-json">"payloadDescription": [        
<strong>        {
</strong>          "type": "Pyro",
          "eventTime": 33.5,
          "vdl": "red comet 5 times",
          "pan": -90,
          "tilt": 180
        }
]
</code></pre>

#### Trigger  `"eventTime"`

The event time is the time, in seconds from start, that the pyro payload fires. There may only be one event time per payload, however there may be many pyro payloads.

#### VDL Support  `"vdl"`

Finale3D's [VDL ](https://finale3d.com/documentation/vdl-effect-glossary/)(Visual Descriptive Language) can be used to define pyro drone payloads. It is used to indicate what product is attached, what color it is, how long it burns, how bright it is and more. This data is exported as part of the VVIZ format and can be visualized directly within Finale3D as part of their other pyro previz.

#### Pan and Tilt `"pan" / "tilt"`

Pan and tilt describe the orientation or mounting direction of a pyro product. Pan is rotation around the vertical axis (or Yaw for a drone) in a clockwise direction. Tilt is a rotation forward. A pan/tilt of (0,0) is considered to be straight up.

***

## Supported Applications

### Finale3D

<figure><img src="../../.gitbook/assets/images (1).png" alt=""><figcaption></figcaption></figure>

#### Exporting to Finale3D

[Finale3D](https://finale3d.com/) is a powerful fireworks design software that is used by industry professionals across the world. Finale3D supports importing VVIZ files.

To import into Finale3D, go to:&#x20;

> File > Import > Import Drone Show...

When imported into Finale3D, the following details are carried over:

* Pyro product VDL
* Pyro mount direction
* Drone Heading
* Drone Position
* LED Color

Finale3D's documentation on the format can be found [here](https://finale3d.com/documentation/vviz-file-format/).&#x20;
