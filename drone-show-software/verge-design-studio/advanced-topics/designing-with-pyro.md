# Designing With Pyro

The Verge Design Studio contains fully-integrated tools to design, visualize, and validate shows with pyro drones.

{% hint style="info" %}
Although the tools covered here are still very helpful for designing drone shows with third-party modules (such as the [Cobra 6M SPFX Module](https://www.cobrafiringsystems.com/6m)), to take full advantage of the automation and workflows available you must use one of Verge Aero's [integrated firing systems](../../../drone-show-hardware/payloads/x1-pyro-module/).
{% endhint %}

## Defining Pyro And Mounting

Each cue can be assigned its own pyro product and mounting direction. When enabled, cues and their associated firing vector are color-coded to make it easier to identify visually. Products are defined via [VDL](https://finale3d.com/documentation/vdl-effect-glossary/). A limited number of products are currently supported, but any can be used when exported to an external application such as Finale3D. Mounting direction can be chosen via a dropdown. Simple directions such as forward/backward, up/down, etc are provided with a custom direction also definable. These directions are relative to the drone and not to the world unless the drones are commanded to point north.&#x20;

<figure><img src="../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

## Cue Triggers

To trigger a pyro cue, a drone must be tracking a slot on an object that is firing a trigger event.

### Sequential Trigger

A sequential trigger leverages the geometry of the attached shape to fire cues in a specific order. Pyro can be fired:

* Left-to-Right
* Right-to-Left
* Out-to-In
* In-to-Out

The triggering of the first and last pyro cue is dependent on the length of the event.

<figure><img src="../../../.gitbook/assets/Sequential_Trigger.gif" alt=""><figcaption><p>A right-to-left sequential trigger event</p></figcaption></figure>

### Simultaneous Trigger

A simultaneous trigger will fire every slot's cue at the same exact time. The length of the event is irrelevant.

<figure><img src="../../../.gitbook/assets/Simultaneous.gif" alt=""><figcaption><p>A demonstration of triggering all products at once</p></figcaption></figure>

### Random Trigger

A random trigger event will fire all present drone slots, but in a pseudo-random order spread equally across the time length of the event.

<figure><img src="../../../.gitbook/assets/Random.gif" alt=""><figcaption></figcaption></figure>

### Alternating Trigger Slots

Trigger events also have support for triggering every N slots rather than all of them. This allows multiple trigger events to be layered, accomplishing more interesting effects.

<figure><img src="../../../.gitbook/assets/Sequential_Criss_Cross_No_Rot.gif" alt=""><figcaption><p>A demonstration of triggering altenating slots from left and right</p></figcaption></figure>

## Pre-viz

The following products are supported for pyro-mounted pre-viz natively:

| VDL                                                               | Description                                                                                                                            |
| ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| [Comet](https://www.youtube.com/watch?v=pYxaxQwWzZI)              | A type of firework star fired into the sky from the ground which leaves a long trail of sparks in its wake as it flies through the air |
| [Strobe](https://www.youtube.com/watch?v=m_cXMcqtTwk)             | A type of firework that produce a series of bright flashes of light in a regular pattern.                                              |
| [Waterfall](https://www.youtube.com/watch?v=-7UKK9POTWg)          | A type of firework that creates the illusion of a waterfall of sparks                                                                  |
| [Mine](https://www.youtube.com/watch?v=rhxB5qGwr_g)               | A type of pyrotechnic device that is fired from a mortar and expels stars and other effects into the air                               |
| [Smoke](https://www.youtube.com/shorts/yIbdQykK78g?feature=share) | A type of pyrotechnic that produces smoke as a result of a chemical reaction. Can be made to be many different colors.                 |

More products will be added in the future, however pyro pre-viz/design applications that support the [VVIZ ](../vviz-format.md)format such as Finale3D or FWsim are capable of visualizing practically any drone-mountable product.

## Pointing Pyro

Pyro mounts will obey drone [yaw control](yaw-control.md) and display guiding arrows to provide feedback during the design process. Ultimately, the only thing the designer needs to be concerned with is that the arrow (and subsequent previz) points in the direction they expect. A simple example of this is in the case that a comet is mounted out of the back of a drone. When configuring a payload target event, the drone must be rotated an additional 180 degrees to point the product as though it were facing out of the front of a drone. Product pointing up or down can not be rotated. Yaw can also be updated on a per-frame basis and create complex sequences.

<figure><img src="../../../.gitbook/assets/ezgif-260edddee7a425.gif" alt=""><figcaption><p>Example of two cues being targeted around a circle. In this example, the drone is shown continuously rotating to point along the tangent of the circle.</p></figcaption></figure>

## Finale3D Support

<figure><img src="../../../.gitbook/assets/images (1).png" alt=""><figcaption></figcaption></figure>

Any performance can be exported to Verge Aero's standard [VVIZ format](../vviz-format.md). This format provides support for LED and pyro drone performances. When imported into Finale3D, the following details are carried over:

* Pyro product VDL
* Pyro mount direction
* Drone Heading
* Drone Position
* LED Color

## FWsim Support

<figure><img src="../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

FWSim documentation can be found [here](https://www.fwsim.com/doc/en/drone_shows.html).

