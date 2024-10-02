# Scene Objects

Scene Objects are nodes that have a physical location within a scene and provide special functionality. Every scene object has a transform that represents a position, rotation, and scale. Scene objects include targets for forming shapes, controlling swarms, performing advanced lighting, and much more.

### 2D Shapes

Shapes that are flat or only have dimensions in the x and y direction. These shapes can still be rotated and scaled to shift slots into the z direction. Modifiers can also be applied to turn 2D shapes into 3D effects. These shapes are well suited to smaller drone counts or as a primitive that is part of a larger, more complex shape.

* Text
* QR Codes
* Circle
* Square
* Ellipse
* Polygon
* Grid
* Fill Circle

### 3D Shapes

Shapes that have depth along with height and width. Simple primitives that can be used as part of more complex shapes.

* Cube
* Sphere
* Scatter Field

### Splines

Splines are a continuous set of linear curves that can be manipulated via anchor points to generate complex shapes. Bezier curves are used extensively in SVG files. A number of primitive shapes built out of bezier splines can be created from the scene object menu. Converting those shapes into a Bezier spline exposes full manipulation.

<figure><img src="../../../.gitbook/assets/image.png" alt="" width="375"><figcaption><p>A Bezier Helix with editable anchor points</p></figcaption></figure>

* Bezier Curve
* Bezier Line
* Bezier Circle
* Bezier Helix

### Advanced Objects

* [Launchpad](launchpad.md)
* Formation Group
* Formation Sequence
* Array Object
* [Show Effect](../show-effects/)
* Flocking Controller

### Volumes&#x20;

Volumes represent 3D sections of space that can be used to inform lighting effects and collision avoidance such as that used in the flocking controller.

* Sphere
* Cube
