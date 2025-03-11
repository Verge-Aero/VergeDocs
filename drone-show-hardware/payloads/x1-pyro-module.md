# X1 Pyro Module

The X1 drone has the capability to comfortably lift 500g with an upper maximum of 700g of additional payload. Depending on the type and size of payload, the X1 is able to support 6 independently-addressible pyro cues.

## The X1 Pyro Module

Verge Aero has developed a custom pyro module that integrates directly with its drone show platform. Coming in at a mere 70 grams, it provides an affordable, lighter-weight alternative to 3rd-party firing systems that unneccesarily include their own power source, radio module, packaging, and independent control software. The goal of the X1 pyro module is to minimize weight, and maximize safety.

| Feature                                              | X1 Pyro Module                                         | Cobra                               | Fire One WMM-4Q                     |
| ---------------------------------------------------- | ------------------------------------------------------ | ----------------------------------- | ----------------------------------- |
| Weight                                               | \~70g                                                  | \~270g                              | \~190g                              |
| Dimensions                                           | 7.25 x 5.5 x 2.75 cm                                   | 10 x 9.2 x 2.4 cm                   | 12.2 x 6.9 x 2.8 cm                 |
| Unique Addresses                                     | > 65K                                                  | 400                                 | 99                                  |
| Radio Redundancy                                     | <mark style="color:green;">✔</mark> \[Sub-Ghz/2.4 Ghz] | <mark style="color:red;">X</mark>   | <mark style="color:red;">X</mark>   |
| Wireless Range                                       | 4+ km LoS                                              | 500m LoS                            | 6 km LoS                            |
| Timecode Support                                     | <mark style="color:green;">✔</mark>                    | <mark style="color:green;">✔</mark> | <mark style="color:green;">✔</mark> |
| Number of Cues                                       | 6                                                      | 6                                   | 4                                   |
| OTA Updates                                          | <mark style="color:green;">✔</mark>                    | <mark style="color:green;">✔</mark> | <mark style="color:red;">X</mark>   |
| Per-Cue Continuity Tests                             | <mark style="color:green;">✔</mark>                    | <mark style="color:green;">✔</mark> | <mark style="color:green;">✔</mark> |
| Remote Arm/Disarm                                    | <mark style="color:green;">✔</mark>                    | <mark style="color:green;">✔</mark> | <mark style="color:green;">✔</mark> |
| Remote Manual Trigger                                | <mark style="color:green;">✔</mark>                    | <mark style="color:green;">✔</mark> | <mark style="color:green;">✔</mark> |
| [Auto-Disarm Systems](x1-pyro-module.md#auto-disarm) | <mark style="color:green;">✔</mark>                    | <mark style="color:red;">X</mark>   | <mark style="color:red;">X</mark>   |

As a weight-saving measure, the module has been potted with a silicon material that provides water-proofing.

<figure><img src="../../.gitbook/assets/Screenshot 2025-01-13 113617.jpg" alt=""><figcaption><p>A close-up of the pyro module</p></figcaption></figure>

### Mounting The Pyro Module

The X1 pyro module is attached via a quick-mount bracket. The bracket is secured via 4 points of contact, each contact uses a push-button interface to make detaching the bracket quick and easy. Because the pyro module is fixed to the pyro bracket, pyro products may be mounted and configured independently from the drone itself. This division is important for two reasons:

1. A certified pyro technician can focus on rigging and mounting the products without the drone present
2. If a drone experiences issues and must be pulled from the show, it becomes incredibly easy to swap the entire pyro payload to a different drone

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption><p>One of the four attach/detach points</p></figcaption></figure>

A single ribbon cable provides an interface between the hivemind control board and the pyro module. This is the only data/power line that must be attached when connecting the pyro module. It may be disconnected/connected when the drone is powered on without any concern that cues will be triggered. Once disconnected, it must be once again armed from the console to enable firing.

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption><p>The mesh ribbon cable providing power and data connections to the X1 companion computer</p></figcaption></figure>

## [Design Studio](../../drone-show-software/publish-your-docs/) Integration

The design studio provides all necessary tools to plan, visualize, and validate drone shows with integrated pyro. When using the X1 pyro module, triggers programmed into the show via the studio are automatically fired as part of the same show file that is in use today. This completely eliminates the need for third-party hardware and software.

### Product Configuration

Each pyro product can be configured independently to define its VDL (Finale3D), mounting direction, and more. All of these fields are exported as part of the [VVIZ ](../../drone-show-software/publish-your-docs/vviz-format.md)format which is supported by third-party software such as [Finale3D](../../drone-show-software/publish-your-docs/advanced-topics/designing-with-pyro.md#finale3d-support).

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Examples of some products defined for a series of drones</p></figcaption></figure>

### Parametric Triggers

Rather than program each trigger independently, shape-based triggers can be generated in the same way lighting events are. Using geometric information, pyro can be triggered based on the order they are placed in a shape. For example, they can automatically be fired counter-clockwise around a circle using a single event.

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>The event settings for a sequential trigger</p></figcaption></figure>

### Pre-Viz

The Design Studio is capable of showing realistic previews of pyro drones at any point in the design process. The visualization accounts for the drone's movement, the way the pyro is mounted, and what effect is being triggered.

<figure><img src="../../.gitbook/assets/Waterfall_Test_2023-10-19_01-08-18.gif" alt=""><figcaption><p>A waterfall effect visualized in the design studio</p></figcaption></figure>

### [Yaw Control](../../drone-show-software/publish-your-docs/advanced-topics/yaw-control.md)

Along with position, the design studio allows drones to be turned to face a specific direction. This can be changed dynamically throughout the show depending on the shape that the drones are traveling on. The simplest example of this, along with trigger control, can be seen below, with a circle that fires comets outward by yawing the drones and firing them in order of the circle.

<figure><img src="../../.gitbook/assets/DirectionTest_2023-10-28_13-29-52.gif" alt=""><figcaption><p>Red comets being fired outward around a circle with a sequential trigger</p></figcaption></figure>

## [Console](../../drone-show-software/verge-console/) Integration

When using the X1 pyro module, a new panel appears within the drone's inspector that exposes important information and tools relevant to the module. The expected product and mount directions are exported as part of the show file.

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>A sample image of the inspector view for pyro with an unconnected E-Match, a bad circuit detection, and two successfully connected E-Matches</p></figcaption></figure>

## Pyro View

Mirroring the functionality of the core device grid view, a new "Pyro View" displays color-coded cue health status in a single view. A greyed-out cue is unused in the show. A red cue is either disconnected or experiencing an error. A green cue means that it is populated, present in the show, and clear of any faults. This makes it very easy to identify which modules are experiencing issues.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>An example of 100 pyro drones with their cue states displayed</p></figcaption></figure>

## Safety Features

#### Manual disarm

The pilot has the ability to disarm _all_ pyro modules across the entire fleet with the push of a button. This will always be the safest option in the case of an emergency. Individual drones may also be selected and disarmed manually, but other, automatic safety features will generally make this capability superfluous.

#### Auto-Disarm

When hundreds or thousands of pyro drones are active and in-flight, it becomes virtually impossible to identify and disable specific pyro modules. The only fallback is to disable _every_ drone simultaneously at the first notice of failure. This weakness is overcome by the X1 pyro module. Crucially, the merger of pyro module and flight control systems allow the drone to make informed decisions and ensures that firing never occurs in any situation it deems unsafe.

The following conditions result in the module being immediately disarmed and powered down:

* Drone enters failsafe due to sensor failure, low-battery, or otherwise
* Drone is commanded to abort the show for any reason, regardless of requested behavior

For a full breakdown of standard Verge Aero safety mechanisms, refer to [this article](../../drone-show-technology/safety.md).

#### Soft-Arm Mechanism

If a pyro module is armed and the attached drone is launched, it conducts a "Soft-Arm" check. No pyro may be triggered, remotely or automatically, until this check is passed. The check only passes if the drone has successfully launched and has not experienced a failsafe. Additionally, if the designed show contains no pyro triggers for the role that is designated to the drone in the show, then it will never be soft-armed. It will fly its role, but with no ability to trigger onboard pyro products.

#### **Circuit Fault Detection**

The pyro module performs multiple checks during bringup and exposes in-depth information to the user about its state. Some fault states include:

| Fault            | Description                                                                                |
| ---------------- | ------------------------------------------------------------------------------------------ |
| Bad PFET         | One or more cues detected a bad PFET                                                       |
| No Power         | 12V power good signal was not present when expected                                        |
| Unexpected Power | 12V power good signal was present when not expected                                        |
| Timeout          | The client failed to issue a command within the timeout period (while not idle or faulted) |
| Comm Failure     | Failed to communicate with the pyro board                                                  |
| CPU Time Error   | The pyro driver is not getting enough CPU time                                             |

Per-Cue circuit testing ensure that the firing system is working properly and can pass errors on a per-cue basis.

#### Overweight Failsafe

The Verge Aero drone show system utilizes a floating, soft-geofence "bubble" that triggers a failsafe if a drone ever strays more than 4 meters from its target position. This provides very early issue detection rather than waiting for it to travel large distances before breaching a fence that circumscribes the entire performance space. If a drone is too heavy, it will attempt to meet the commanded flight paths, but will fail within seconds. Without such a mechanism, other systems would continually lag behind their target position and may collide with other drones.

### Mounting Pyro Product

The flat metal sheeting protects the underside of the drone from heat and evenly distributes recoil across the chassis. It comes with affixed cable clips to simplify wire routing. It is absolutely imperative that wires be kept taut and cleanly routed in order to avoid situations where they become tangled in the drone's rotors.
