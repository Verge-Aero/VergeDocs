# Spline

A spline is a curve or collection of continuous curves that are defined by a set of (in this case) 3D points. Unlike point clouds, splines are an excellent type of geometry for drone formation definition because they can be split up infinitely to support any number of drones.&#x20;

## Spline Shapes

There are multiple spline-based shapes that can be generated/manipulated with simple parameters. Any of these shapes can be converted into an "Editable Spline" by selected the associated button in the spline edit toolbar.

These shapes include:

* [Bezier Circle](bezier-circle.md)
* [Bezier Helix](bezier-helix.md)
* [Bezier Line](bezier-line.md)

## Color

Splines can be assigned solid colors, or gradients. If a gradient is assigned, then the gradient will be applied along the spline in order from the start to end.

## Editing Splines

When selecting one or more splines, spline shapes, or compound splines, a toolbar will appear on the top of the scene view. This toolbar provides quick ways of manipulating splines, editing geometry, and managing groupings. Buttons become enabled/disabled based on the current selection and state of the splines.

<figure><img src="../../../../.gitbook/assets/image (6).png" alt=""><figcaption><p>The spline toolset panel</p></figcaption></figure>

{% tabs %}
{% tab title="Convert" %}
These buttons are responsible for changing a shape into another shape container. Some tools and options are not available unless a bezier shape is converted into an editable spline or the shape is a compound spline.

<details>

<summary><img src="../../../../.gitbook/assets/image (10).png" alt="" data-size="original"> To Editable Spline</summary>

Convert a bezier shape into a form that can be manually editable. This will cause the shape to lose its unique parameters in favor of a generic spline

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (46).png" alt=""> To Compound Spline</summary>

Convert a bezier spline or shape into a compound spline, supporting multiple splines in a single shape

</details>
{% endtab %}

{% tab title="Spline Tools" %}
This set of tools provide high-level ways of manipulating one or more splines. They also expose ways of grouping/ungrouping splines into and out of compound splines.

<details>

<summary><img src="../../../../.gitbook/assets/image (47).png" alt=""> Center Anchor</summary>

Automatically shift the shape's centroid to be the average of all spline control points

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (48).png" alt=""> Shift Anchor</summary>

Enter a mode where the anchor can be shifted while keeping the spline's geometry world-locked. To stop anchor shifting, the button must be toggled again.

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (49).png" alt=""> Reverse</summary>

Reverse the order of the points in the spline. This will result in an identical spline, but with start and end points reversed. Useful for ensuring that lighting effects move in the correct direction

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (49).png" alt=""> Reverse</summary>

Reverse the order of the points in the spline. This will result in an identical spline, but with start and end points reversed. Useful for ensuring that lighting effects move in the correct direction

</details>

<details>

<summary> <img src="../../../../.gitbook/assets/image (50).png" alt=""> Duplicate</summary>

Duplicates the selected spline/s. This only works for compound splines. The duplicated spline will appear as a new sub-spline.

{% hint style="warning" %}
Spline must be converted to a compound spline to use the Duplicate tool
{% endhint %}

<figure><img src="../../../../.gitbook/assets/ezgif-5a69d8fdd1f070.gif" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary> <img src="../../../../.gitbook/assets/image (52).png" alt=""> Merge (Group)</summary>

Combines the selected splines into a single compound spline.&#x20;

</details>

<details>

<summary> <img src="../../../../.gitbook/assets/image (53).png" alt=""> Separate (Ungroup)</summary>

Removes the selected splines from their current compound spline and puts them into separate standalone splines.

</details>

<details>

<summary> <img src="../../../../.gitbook/assets/image (54).png" alt=""> Close</summary>

Forces the spline to be a complete loop. The endpoint will be shifted to be placed on top of the start point.

</details>

<details>

<summary> <img src="../../../../.gitbook/assets/image (55).png" alt=""> Open</summary>

Allows the spline start and end points to be separated

</details>

<details>

<summary> <img src="../../../../.gitbook/assets/image (56).png" alt=""> Delete</summary>

Deletes the currently selected anchor point, segment, or spline

</details>
{% endtab %}

{% tab title="Edit" %}
This button array provides a way to choose selection mode as well as entering/exiting spline edit mode. Edit mode must be entered to modify spline anchor points or use the geometry tools

<details>

<summary><img src="../../../../.gitbook/assets/image (57).png" alt=""> <img src="../../../../.gitbook/assets/image (58).png" alt=""> Edit Mode (Exit Edit Mode)</summary>

Enter edit mode and allow geometry to be selected and manipulated. The button will toggle to an X when active and must be clicked again to exit edit mode.

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (59).png" alt=""> Anchor Point/Vertex Selection Mode</summary>

Enter anchor point selection mode where only anchor points (points that lie directly on geometry) can be selected

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (68).png" alt=""> Control Point/Handle Selection Mode</summary>

Enter control point selection mode where any control point can be selected and shifted

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (69).png" alt=""> Segment Selection Mode</summary>

Enter segment selection mode where any segment can be selected and shifted

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (70).png" alt=""> Spline Selection Mode</summary>

Enter spline selection mode where any spline can be selected and shifted

</details>
{% endtab %}

{% tab title="Geometry Tools" %}
<details>

<summary><img src="../../../../.gitbook/assets/image (60).png" alt="" data-size="original"> Smooth Geometry</summary>

Takes all selected geometry and sets it to be as smooth as possible by adjusting spline control points to be tangential and parallel

<figure><img src="../../../../.gitbook/assets/ezgif-53150e76cb59a7.gif" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (61).png" alt=""> Straighten Geometry</summary>

Takes all selected geometry and sets it to be as straight or sharp as possible by adjusting spline control points to be coincident (or on top of eachother) for each anchor point

<figure><img src="../../../../.gitbook/assets/ezgif-56ca5bd2bb7cc4 (1).gif" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (62).png" alt=""> Extrude Geometry</summary>

Takes selected segment (or vertex if on an endpoint) and creates a new line on each side so that it may be pulled away without disturbing surrounding segments

<figure><img src="../../../../.gitbook/assets/ezgif-7527c947c9b5e0.gif" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (60).png" alt="" data-size="original"> Merge Geometry</summary>

Fuses two selected endpoints to form a single spline

<figure><img src="../../../../.gitbook/assets/ezgif-502c764f09758b.gif" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (60).png" alt="" data-size="original"> Split Geometry</summary>

Takes selection and breaks its endpoints from the containing spline. This will create new splines to properly contain the new separated segments.

{% hint style="warning" %}
Spline must be converted to a compound spline to use the Split tool
{% endhint %}

<figure><img src="../../../../.gitbook/assets/ezgif-59089b17909faf.gif" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary><img src="../../../../.gitbook/assets/image (60).png" alt="" data-size="original"> Subdivide Geometry</summary>

Takes the selected segments and evenly subdivides them, inserting a single new vertex per-segment for every click

<figure><img src="../../../../.gitbook/assets/ezgif-58aebd0f8e1314.gif" alt=""><figcaption></figcaption></figure>

</details>
{% endtab %}
{% endtabs %}

## Slotting Control

<figure><img src="../../../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

## Pivot Weighting

The design studio leverages geometric information to make decisions around where to place slots. In the case of a spline, harsh angles or "corners" can be treated specially and the software well make sure that a drone is placed exactly on the corner. This will maximize detail and definition.

<figure><img src="../../../../.gitbook/assets/image (63).png" alt=""><figcaption><p>Pivot weighting on (Left) and off (right)</p></figcaption></figure>

`Use Pivot Weighting:` Enable/Disable the use of pivot weighting in the slot solution

`Pivot Angle Threshold:` The angle (in degrees) that a corner must be _below_ in order for it to be treated as a pivot point

## Partial Spline

The slot solver can be set to use _only a portion_ of a spline. This is particularly useful in combination with animating the slot offset field if you want to move a group of splines along a path.

{% hint style="warning" %}
You must disable pivot weighting in order to use partial spline functionality
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

`Use Partial Spline:` Enable/Disable the use of a partial spline

`Start Percent (%):` The location (in percent, where 0% is the start and 100% is the end) to start the spline&#x20;

`End Percent (%):` The location (in percent, where 0% is the start and 100% is the end) to end the spline&#x20;

<figure><img src="../../../../.gitbook/assets/ezgif-443043bf055540.gif" alt=""><figcaption><p>Shifting end percent from 100% to 0%</p></figcaption></figure>

## Hull Slot Solver

Along with the standard linear solver, there is also a mode that allows a spline shape to be filled in.

<figure><img src="../../../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/ezgif-503224d8a2bdb1.gif" alt=""><figcaption></figcaption></figure>

### **Hull Projection Axis**

* **Description**: Specifies the axis along which the spline is projected to compute the 2D hull for slotting.
* **Options**:
  * **X**, **Y**, **Z**: Choose the axis orthogonal to the hull's plane. Used to flatten 3D splines into a 2D working surface.

### **Slot Mode**

* **Description**: Determines the algorithm used to generate the filled surface inside the spline’s hull. This affects how vertices are distributed across the area enclosed by the projected hull.
* **Options**:
  * **Scaled Fit**
    * Fills the convex or concave polygonal region and then _stretch_ them so that points touch the boundary of the shape
    * Ideal for structured interpolation and clean, regular fills.
    * Can set the number of columns/rows directly or define a density for placement
  * **Poisson Distribution**
    * Inserts vertices using a Poisson disk sampling method.
    * Ensures randomly distributed points with a minimum distance between them, avoiding clumping while preserving uniformity.
    * Best suited for naturalistic or non-uniform point distributions (e.g., organic modeling, scattered elements).
    * Row and scanline settings are ignored in this mode.
    * Density controls how close/far points are distributed
    * Random seed can be tweaked to get slightly different distributions
  * **Bounded Grid**
    * Fills the hull area with a regular grid of points, clipped to the boundary of the projection.
    * Produces a structured mesh of evenly spaced rows and columns, spacing is identical vertically and horizontally.
    * Works well for mechanical or architectural shapes requiring evenly spaced subdivisions.
    * Density controls how close/far points are distributed
