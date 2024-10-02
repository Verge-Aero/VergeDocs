# Launchpad

A launchpad is the core object that used to design a drone show. Launchpads are drone containers and represent the starting positions of those drones in the show. Unlike other objects, launchpads _must_ be located on the ground and have a locked y position component. Launchpads include a drone control channel that exposes functionality for launching drones, tracking scene shapes, and returning the drones to their landing positions.

<figure><img src="../../../.gitbook/assets/image (2).png" alt="" width="345"><figcaption><p>A screen capture of the launchpad inspector</p></figcaption></figure>

#### Drone Count

The drone count field can be used to adjust the total number of drones in the launchpad. The drone count can be changed at any time and will propogate through the show design. The drone count is also automatically capped based on the formation shapes and the max number of drones that can be safely placed in that formation to maintain launchpad density.

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption><p>A grid launchpad in the middle of a staggered launch sequence</p></figcaption></figure>

#### Formation

A pool of shapes are available&#x20;

* Grid
* Circle
* Rectangle
* Polygon
* Arbitrary

#### Drone Spacing

The launchpad provides information about the distance between the closest two drone launch positions. This simplifies adjusting parameters to reach a desired density. In the case where spacing is too low to safely launch, an error message is shown and the render fails to run. As spacing is manipulated, the launch event will automatically adjust and scale in length to accomodate the additional or reduced time involed in safely launching the drones.

<div align="center" data-full-width="true">

<figure><img src="../../../.gitbook/assets/image (5).png" alt="" width="495"><figcaption><p>An error message indicating that the launchpad spacing is insufficient for launch</p></figcaption></figure>

</div>

#### Overflow Shape

Optionally, an overflow shape can be defined on a launchpad. In the case where a targeted shape does not have enough available slots to place the drones, excess drones are automatically moved into the overflow shape.

## Agent Definition

Each launchpad also exposes parameters that can be used to configure the contained drone type and attached payloads. By default, a drone is assumed to be equipped with an standard RGBW LED. This section becomes important when configuring a show for using [pyro](../../../drone-show-technology/fireworks-and-drone-shows.md) or enabling [yaw control](../advanced-topics/yaw-control.md).

<figure><img src="../../../.gitbook/assets/image (4).png" alt="" width="335"><figcaption></figcaption></figure>
