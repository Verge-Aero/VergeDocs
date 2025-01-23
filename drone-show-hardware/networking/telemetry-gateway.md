# Telemetry Gateway

The [X1](../drones/x1.md) and [X7](../drones/x7.md) integrate a dual-band radio to support any point-to-point read or write operations. It is configured to provide a good balance between high-reliability and high-bandwidth.

### What It Is Used For

The telemetry gateway provides an up and downlink for the majority of data structures and commands. It is used for:

* Telemetry
* Individual Drone Commands
  * Setting safeties
  * Setting individual light modes
  * Calibration
  * Motor Tests
  * Etc.
* Uploading show files
* [Updating drone firmware](../../drone-show-software/verge-console/firmware-vpkg-system.md)
* Live-Lighting
* More

#### Dual-Band Operation

Both bands can be used simultaneously, but only one is used in the current software package. Support for dual-band operation is intended to be added in the near future.
