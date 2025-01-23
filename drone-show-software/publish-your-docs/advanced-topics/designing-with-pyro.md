---
hidden: true
---

# Designing With Pyro

The Verge Design Studio contains fully-integrated tools to design, visualize, and validate shows with pyro drones.

{% hint style="info" %}
Although the tools covered here are still very helpful for designing drone shows with third-party modules (such as the [Cobra 6M SPFX Module](https://www.cobrafiringsystems.com/6m)), to take full advantage of the automation and workflows available you must use one of Verge Aero's [integrated firing systems](../../../drone-show-hardware/payloads/x1-pyro-module.md).
{% endhint %}

## Defining Pyro And Mounting



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

Pyro mounts will obey drone [yaw control](yaw-control.md) and display guiding arrows to provide feedback during the design process.&#x20;

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

