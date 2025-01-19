# Safety

Verge Aero's system seeks to minimize human error and risk by maximizing automation and restricting user freedom to the core functionality required for performing a drone show. By design, the system leans toward over-sensitivity to error states and seeks to reject operation at the earliest state possible. Rejection states can occur at multiple points in the pipeline: at design-time, during pre-flight, at mission execution, and during a mission.

Verge Aero follows generally accepted best practices for robust software development. These include code reviews, unit testing, continuous integration, etc. Before entering a new version of any portion of the system into production, the entire system is validated via simulated integration tests and real-world flights. Verge Aero hardware, such as the [X7](../drone-show-hardware/drones/x7.md) drone, undergoes multiple manufacturing tests to ensure that components are in working order before they are distributed to customers.

This article provides an overview of the validation process that occurs continuously throughout the show production pipeline and as part of the release strategy when updates to the software or hardware are made. Additionally, this article summarizes safety features that ensure that the risk of human injury and structural damage are minimized.

### Verge Aero Drone Show System Components

Verge Aero’s drone show system software stack consists of the following elements:

* Verge Aero's [Design Studio](../drone-show-software/publish-your-docs/)
  * A desktop application with an easy-to-use interface
  * Used to design, validate, and generate drone show missions
* Verge Aero's Web Portal
  * A web-based portal that handles converting shows exported from the design studio into flyable missions
* Verge Aero's [Console](../drone-show-software/verge-console/)
  * A desktop application that typically runs on a laptop on-site
  * Used to configure, deploy, and monitor drone show missions
* Hivemind
  * Onboard companion computer responsible for monitoring drone health, choreographing missions, managing peripheral payloads, and executing safety procedures
* [PX4](autopilot/px4.md)
  * Open source autopilot stack that is responsible for sensor fusion, driving motor output, and executing a flight mission
  * Nearly unmodified from its source

## Operational Validation

Operational validation is defined as any validation that occurs as part of the show design and deployment process. This is not conducted manually by Verge Aero, but via automated means or as part of the show production process conducted by the end user.

### Verge Aero Design Studio Output Validation

Any show designed within the design studio is subject to a set of automatic testing criteria to ensure that the generated mission is well-formed, within physical constraints, and obeys regulatory requirements. If any of the tests resolves in failure, then the software does not allow the user to export the mission description. These tests are performed as part of a “rendering” process where the swarm is simulated and the mission is played back virtually. This must occur before export is possible.

| Test                           | Description                                                                                                                                           |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Altitude Validation            | Ensure that no drone exceeds max allowable altitude (depending on jurisdiction). Ensure that no drone flies below the ground plane.                   |
| Trajectory Validation          | Ensure that flight paths are well formed and timing information never results in waypoints being scheduled before previous waypoints are complete.    |
| Velocity Validation            | Ensure that flight trajectories do not command velocities exceeding physical limits in an upward direction, downward, and on the horizontal plane.    |
| Acceleration Validation        | Ensure that flight trajectories do not command accelerations exceeding physical limits in an upward direction, downward, and on the horizontal plane. |
| Inter-drone Spacing Validation | Ensure that at any point in a show, no two drones travel within a safe distance from one another.                                                     |
| Land Validation                | Ensure that every drone returns to a landing position as part of its mission.                                                                         |
| Flight Time Validation         | Ensure that every mission results in flight that does not exceed the maximum flight time the batteries allow.                                         |
| Geofence Validation            | Ensure that every mission occurs within the flight operation volume. Ensure drones do not exit their generated geofence boundaries.                   |

#### Mitigation Strategy

Any test failure rejects export. The user may not generate a flyable mission file until the tests pass.

### Verge Aero Cloud Services Validation

After a show is exported from the [design studio](https://wiki.droneshow.software/wiki/Verge_Design_Studio), it must be uploaded to Verge Aero’s web portal. This web portal is responsible for conducting additional automatic checks and, crucially, allows Verge Aero to have oversight regarding where users are seeking to execute shows. Geofences are checked against airspace classifications and, in the case that the show is planned in any controlled airspace, Verge Aero personnel verify that the user has obtained proper clearance before allowing missions to be generated. This ensures that Verge Aero drones will never fly in unauthorized locations. Once approved and validated, a show file is generated that can be used to execute a mission.

### Verge Aero Console Input Validation

The console application performs multiple tests on a mission file when it is loaded to catch any possible issue that may have occurred during export from the design studio or due to accidental/malicious modification of show files.

| Test                      | Description                                                                                                                                        |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Light Data Validation     | Ensure that a light data stream is included for every drone and that it is triggered appropriately                                                 |
| File Integrity Validation | Ensure files match linked md5 hashes                                                                                                               |
| Trajectory validation     | Ensure that flight paths are well formed and timing information never results in waypoints being scheduled before previous waypoints are complete. |
| Land validation           | Ensure that every drone returns to a landing position as part of its mission.                                                                      |
| Flight time validation    | Ensure that every mission results in flight that does not exceed the maximum flight time the batteries allow.                                      |
| Geofence Validation       | Ensure that every mission contains a geofence and that it matches or is within the overall flight volume                                           |

#### Mitigation Strategy

Any test failure rejects import. The user may not open a mission file until the issues are resolved.

### Verge Aero Console Pre-flight Validation

Once a mission is loaded, the user must follow a setup procedure to get the drones ready for flight. Drones must be placed in geo-locked coordinates associated with the launch positions set within the design stage. A pre-flight checklist embedded in the console must also be followed and signed off on before the fleet may be armed. Drones will not be assigned roles within the show unless they pass health checks. Additionally, if the drones are healthy and assigned roles, but become unhealthy preceding a takeoff routine, they refuse to arm. This is described in the "Hivemind Pre-flight Validation” section.

#### Actively-Enforced Console Health Checks

| Check                          | Description                                                                                                    | Mitigation Strategy                                                                                                        |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| RTCM Data Validation           | Ensure that an RTK base station is attached, it is surveying, and it is operating with sufficient GPS accuracy | Warn user and disallow flight                                                                                              |
| Drone Configuration Validation | Ensure the drone configuration has been synchronized with the console configuration. This includes             | Warn user of configuration divergence. Reject assignment of that drone                                                     |
| Role Validation                | Ensure that no two drones are assigned the same role in the show.                                              | If two drones are assigned the same slot, then reject the drone farthest away from the role’s geo-coordinate               |
| Drone Sensor Validation        | Ensure that drones are not exhibiting sensor failures and the estimator is functioning as expected             | Warn user of poor drone health. Reject assignment of that drone                                                            |
| GPS Accuracy Validation        | Ensure that the drone is reporting RTK Fix or low RTK float accuracies                                         | Warn user of poor GPS quality. Low GPS quality results in inability to prepare launchpad since position estimations drift. |
| Drone Firmware Validation      | Ensure that the drone firmware and parameters match expected versions                                          | Warn user of firmware mismatch. Allow user to make a decision whether to launch or not                                     |

#### Procedural Validation

Verge Aero provides documentation that includes recommendations for pre-flight testing and operational procedures to decrease risk.

**Hover Test**

The design studio allows special test routines to be generated that can be performed before full show execution to ensure that drones are performing as expected. The hover test is a short launch, hover, and land that prove that positioning is stable and that motors are functioning properly.

**Motor Test**

Rotors can be spun up at low speeds such that the fleet remains stationary. They may be observed for appropriate rotational direction. Damaged rotors may either not spin at all or make audible sounds such as “grinding” or “ticking”.

**Subset Test**

It is highly recommended to send a small number of drones (\~4) that cover the extents of the performance volume before flying a full show. This is especially true when operating in complex, urban environments where RF interference is likely. A subset test allows a low risk validation that RTCM data is being received successfully. If RTCM data is not being received during a subset test, then the resulting GPS accuracy decay will not result in collisions as they are spaced well beyond basic GPS precision.

**Show File Integrity Test**

Once assigned a role in the show, an optional test may be run from the console where each drone quickly steps through its mission and checks to ensure that it is error-free.

### Hivemind Pre-flight Validation

Along with the active checks provided by the Verge Aero Console, the companion computers aboard each drone perform their own pre-flight checks. These checks occur persistently and the results are displayed in the Verge Aero Console application so that the pilot may take appropriate action. The checks are also performed at the moment a request is made to arm the drone and the failure of any single preflight check results in an arm denial.

#### Onboard Preflight Health Checks

| Check                          | Description                                                                                                      |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| Sensor Health Validation       | Ensure that sensors are reporting valid data and the pose estimation is within expected errors                   |
| Launch Position Distance Check | Ensure that the drone is within a maximum distance (< 1 meter) from its expected starting position               |
| Show Schedule Check            | Ensure the show is being triggered within a valid date-time. Time is matched against GPS time.                   |
| Drone Battery Validation       | Ensure that the current battery charge supports the mission’s flight length.                                     |
| GPS Accuracy Validation        | Ensure that the drone is reporting RTK Fix or low-value RTK float accuracies.                                    |
| Show Cue Check                 | Ensure that the show trigger Cue ID matches the loaded show. Stops an incorrect show/mission from being executed |

## Developmental Validation

### Full System Integration Tests

As Verge Aero’s drone show system software stack consists of many complex, individual components, we rely on full system integration tests to determine whether changes to any one component of the stack should be integrated. The acceptance criteria for any change is based on two tiers of testing.

#### Verge Aero Simulation Framework

Verge Aero has developed an automated test routine that is able to build and deploy firmware, load test show files, and remotely configure and execute a show by using the entire system stack in the same way that a user would. The only simulated component exists within the FC. The FC can be entered into SIH (Simulation-In-Hardware) mode. In this mode, sensor input is simulated and a physical model is applied to the motor output to drive changes in the sensor input. Simulated sensors include the GNSS module, IMUs, magnetometers, and barometers. The test rig consists of a full system setup with base station hardware, a PC running the console software, and N drones running in SIH mode. The more drones added to the rig, the fewer the total required missions to support our reliability requirements.

#### Field Testing

Following a successful result from the simulation framework, real-world tests are conducted. The only systems that are being tested with real-world flights are the motors and drone sensors. As these systems do not change between software modifications, flights at scales of around 200 agents are sufficient for validating that simulations match real-world scenarios. It should be noted that over 100K total flight hours have been conducted with Verge Aero drone systems and it has been validated that simulations are a very good match with real-world operations. Over the course of the system’s usage, there have been no breaches of the operational safety volume, and there have been no major incidents.

Every flight is comprehensively recorded to an onboard SDCard. In the case of flight failure, Verge Aero has the ability to replay the drone’s state and diagnose the cause of the failure. Flight logs include battery information, sensor states, position, motor output, GPS analytics, and much more.

## Safety Systems

Once launched, there are redundant automatic and manual systems for detecting and mitigating issues. To the best of its ability, the drone will make use of redundant sensor packages and estimators to maintain a valid position estimate. In the case of any exception that hinders a drone’s ability to execute its mission, the most likely strategy involves invoking the onboard flight termination system (FTS).

### Definitions

1. FMU - Flight Management Unit
2. CC - Companion Computer
3. FTS - Flight Termination System
4. [PX4](autopilot/px4.md) - An open source autopilot stack

### FTS Description

Definition of FTS Termination States:

Smart RTH

_Executes a pre-planned, deconflicted flight path that ensures collision-free return of a fleet to its starting point. State must be executed across the entire swarm. Is managed by the CC._

_Smart RTH plans are generated at the same time as the main mission via the same mechanisms. The plans are subjected to the same validation procedures as the main mission. RTH procedures are planned at 30 second intervals. Triggering RTH at any point will cause the swarm to take the next available RTH branch plan._

Auto Land Mode

_Halt global horizontal displacement and descend at a constant maximum speed that maintains stability. Horizontal position is actively enforced via the GNSS system. Barring physical damage, horizontal displacement can be ensured to be below 1-2 meters. Entirely managed on the FMU._

Descend Mode

_Attempt to halt horizontal displacement and descend at a constant maximum speed that maintains stability without the assistance of GPS. Entirely managed on the FMU._

Shutdown

_Full system power termination by executing a failsafe on the smart battery (X7) or soft-termination of the motors (X1). Can be executed from the FMU or the CC/FTS._

The concept of an “FTS” on Verge Aero’s drone platforms are merged with the functionality of the companion computer. The job of this subsystem is to handle error states across the system as a whole and deploy mitigation strategies to ensure that the drone safely ends its performance if necessary and never exits the ground risk buffer.

The FTS may be engaged in many situations. A high-level flow chart covering these cases and the resulting states can be seen in figure 1.1. The FTS loop may cause a mission exit and state change in the following cases:

* The FMU is no longer sending heartbeats to the CC
  * Shutdown is initiated
* GNSS is no longer valid
  * Position data is no longer received by the CC
  * Shutdown is initiated
* FMU is no longer “healthy” or in a fit state for automated flight
  * Estimator is flagged as invalid
  * Battery is too low
  * Total sensor loss
  * Etc
* The drone has exited the performance volume
  * If within the contingency volume, land. Otherwise, shutdown

GNSS Validity Determination

The GNSS module aboard the X1/X7 provides a number of metrics that can be used to gauge validity. Additionally, the FMU provides a validity metric for global position based on sensor fusion estimate covariances. If validity is false, then the drone will enter into a failsafe.

\[GNSS] Accuracy Metrics: Via the UBX protocol, the GNSS module regularly reports an estimated horizontal and vertical accuracy in millimeters. If RTK data is being relayed properly, this number is expected to be around 10 mm for both horizontal and vertical measurements. The total accuracy tends to cap out at 2.4 cm. Any unexpected deviation beyond “acceptable” errors are considered to be invalid (> 10 m).

\[GNSS] GPS Fix Type: The GNSS module reports a GPS fix type that is associated with its general accuracy. Any fix type below 3D GPS is unusable and considered to be invalid.

* No GPS
* 2D GPS
* 3D GPS - Minimum acceptable
* DGPS
* RTK Float - Typical Operation
* RTK Fix - Typical Operation

\[GNSS] GPS Noise and Jamming Indicator: The GNSS module reports both GPS noise and a jamming indicator that can be used to gauge whether external GPS conditions are poor.

\[FMU] GPS Behavior limits: The FMU performs multiple configurable checks to decide whether a GNSS estimate is valid. These include:

* Minimum satellite count (6)
* Maximum allowed position dilution of precision (2.5)
* Maximum allowed horizontal position error (3 m)
* Maximum allowed vertical position error (5 m)
* Maximum allowed speed error (0.5 m)

\[FMU] Estimator Flags: Global position is reported to the FMU at a rate of 5 Hz. Velocity is fused as part of a high frequency (> 100 Hz) EKF position estimate which also includes input from onboard IMUs, magnetometers and barometers. Positional movement that does not match the instantaneous movement indicated by onboard sensors will result in rising variances/errors and enter the drone into an estimator failure state which results in failsafe.

Manual FTS Trigger

The typical activation of the FTS relies on autonomous methods. In a swarm of more than 1000 agents, it is infeasible to identify, target, and trigger a failsafe on a single agent in any meaningful way. Automatic detection and mitigation is always the safest, most dependable route. There are, however, paths to manually trigger the FTS on individual drones as well as the entire fleet at once. Figure 1.3/Figure 1.4 demonstrates the paths available to perform manual and automatic triggers. Any single or set of drones can be selected and terminated via the GCS over the primary radio. In addition, a standalone, redundant trigger box can be used to fire a fleetwide trigger that has no reliance on the GCS once initialized. The box must be connected to the GCS and a mission must be loaded before it is operable. A 32-bit security key is transferred that ensures that no external trigger box could be used for malicious purposes. Once transferred, the trigger box may be disconnected and function independently without any communication to the GCS. While connected, the GCS will continue to get health status from the trigger box to verify to the pilot that it is functioning as desired and that the data is synchronized. Any number of trigger boxes may be connected if additional redundancy is desired. Drones continually receive data packets from the long-range radio which function as a heartbeat. If this heartbeat is absent for more than 5 seconds, the drone flags the link as invalid and reports the state to the GCS.

