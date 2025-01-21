# Comparisons To Third-Party Systems

There are some important factors when considering how safety differs between drone show systems. The current landscape of drone show technology is highly fragmented, shockingly unregulated, and severely lacks in standards. Unfortunately, this often means that shortcuts are taken when building products or developing software. Product features may be provided at the cost of safety or reliability. Pilot error can be minimized through smart design decisions and automation. Proper&#x20;

### Estimator Redundancy <a href="#pdf-page-t78ensyf4xb9yrk4m25e-estimator-redundancy" id="pdf-page-t78ensyf4xb9yrk4m25e-estimator-redundancy"></a>

All Verge Aero drones, including the X1 and X7, contain sensor redundancy. Many other drones contain a single sensor and thus run a single estimator. There is no estimator fallback. This is a shocking oversight and can directly lead to a "flyaway" at any time, regardless of whether the drone experiences damage or a collision. The X7 runs 4 estimators simultaneously with its 2 IMUs. The X1 runs 9 estimators simultaneously with its 3 IMUs. As long as one of the estimators remains valid, the drone's state estimate will continue to be accurate.

### Modern PX4 Improvements - Estimator Stability <a href="#pdf-page-t78ensyf4xb9yrk4m25e-modern-px4-improvements-estimator-stability" id="pdf-page-t78ensyf4xb9yrk4m25e-modern-px4-improvements-estimator-stability"></a>

While the inclusion of fallback sensors are very important, there are also a host of bug fixes, improvements, and major safety features introduced in PX4 over the years since its release. Some of these improvements include:

* Support for Multi-EKF, the mechanism that even allows multiple sensors to be leveraged simultaneously was included in version 1.12. If the drone's software is based on a version previous to this version, then the presence of more than one sensor set is meaningless.
* EKF-GSF, or a fallback mechanism that leverages GPS velocity should all magnetometers fail
* Vastly improved takeoff in magnetically compromised environments
* Active, automatic sensor calibration
* Multiple height source fusion
* Much more

Verge Aero has been continually committed to providing up-to-date autopilot firmware that takes advantage of the latest safety features. The X1 and X7 currently support the latest PX4 version as of Q4 2024 ([1.15](https://docs.px4.io/main/en/releases/1.15.html)) and this article's authoring. Many of the other drones flying drone shows are based on old firmware as the cost of maintaining the cutting edge can be expensive. Additionally, companies that provide software-only must be able to deploy that software to a broad range of hardware platforms with differing processors, memory-limitations, sensors, etc. It becomes a nightmare to ensure that every release of the autopilot supports every hardware platform. As we develop both software and hardware, this becomes a much more streamlined and focused endeavor.

### Dynamic Soft Geofence - Early Issue Detection <a href="#pdf-page-t78ensyf4xb9yrk4m25e-dynamic-soft-geofence-early-issue-detection" id="pdf-page-t78ensyf4xb9yrk4m25e-dynamic-soft-geofence-early-issue-detection"></a>

One of the most important ways to avoid drones coming dangerously close to the audience is to begin grounding maneuvers as early as possible when a failure occurs. It is problematic that the majority of firmwares wait until the soft geofence is breached (which is nearly at the show's most outside boundary) before initiating an RTL or land command. This means that its vertical position is maintained as the drone hurtles toward the geofence and action is taken at the last possible moment.

From the moment a drone launches until the moment it touches the ground, the X1/X7's hivemind companion computer provides a 4 meter-radius 3D "bubble" that the drone must stay within in order to continue flight. This bubble moves along the flight plan's target trajectory and provides a _very_ early detection of any kind of divergence from expected flight position. This provides early detection for a multitude of issues such as GPS jamming, GPS spoofing, airframe damage, motor failure, sensor issues, and more. Depending on the flight space, this can lead to the detection of issues and subsequent action more than 100 meters before arriving at the hard geofence or the point in time that other systems take action.

<figure><img src="https://open.gitbook.com/~gitbook/image?url=https%3A%2F%2Flh7-rt.googleusercontent.com%2Fdocsz%2FAD_4nXecsLagLYGuM2nkMeL5HO4RXOuwVGW-lsoKuROjpQabXyhxM8UhEW2xI6anwNbZRQyLJ6Uurig7Xo2WfxizyjdWYTCWfkD-fw8xc3XvZ_R97D2SKHMpl8A7HqECAVeWeENp6KKhUIE0YjcMHtvSOETfyVaj%3Fkey%3DCycmD5XzuOp_sKnPLZuoAQ&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=a33b85ac&#x26;sv=2" alt=""><figcaption><p>Shows the dynamic soft geofence used for every Verge Aero show performance</p></figcaption></figure>

## Pilot Error - Show Space <a href="#pdf-page-t78ensyf4xb9yrk4m25e-pilot-error-show-space" id="pdf-page-t78ensyf4xb9yrk4m25e-pilot-error-show-space"></a>

In a drone show incident that occurred in 2024, an investigation found that the pilot accidentally shifted the show space and the geofence into a location that put the audience directly in harm's way. Allowing a pilot to significantly manipulate the show plans without limits is concerning as it invalidates all of the planning that ensures that drones do not fly over an audience or within a safe distance. The ability to "rotate" the show space is especially problematic as small adjustments may compound into massive swings of the geofence coordinates as distance grows from the show's center point. When a show is created in the Verge Design Studio, the geofence and associated safe space is generated automatically and may not be modified by the pilot except within a very small offset.

### Pilot Error - Launch Sequence <a href="#pdf-page-t78ensyf4xb9yrk4m25e-pilot-error-launch-sequence" id="pdf-page-t78ensyf4xb9yrk4m25e-pilot-error-launch-sequence"></a>

In many drone show systems the launch sequence is configured and executed, whether automatically or manually, independently from the pre-planned and validated show trajectories. This provides additional room for error and is part of the explanation as to why the Lake Eola show experienced mass collisions. In the Verge system, the launch sequence is not separated from the rest of the show sequence and cannot be modified by the pilot in any way. It is validated and deconflicted by both the design studio (on export) and the console application (on import). There is no chance that this type of failure will occur with X1s or X7s.
