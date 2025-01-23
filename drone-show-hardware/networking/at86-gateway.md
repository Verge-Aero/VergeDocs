# Long-Range Gateway

All Verge Aero drones contain a long-range, low-bandwidth radio that is used to send mission-critical messages. The radio, in practice, is _very_ low bandwidth and the data rates that we use are in the low, single digit kbit/s range, or even less. The upside, however, is that the drones are essentially guaranteed data reception in line-of-sight scenarios. The technology has a theoretical range of more than 10 Km, but this has never been tested in practice with the [Verge Aero](../../) platform. In practical scenarios, there has never been a hardware-driven loss of the long-range data link.

The [X1 ](../drones/x1.md)and [X7](../drones/x7.md) integrate a long-range radio to support mission-critical, broadcast data payloads. This is the _only_ link necessary to successfully execute a show. A loss of all other data transfer methods after a show has been launched will still lead to a successful mission.

The radio module provides continuous frequency coverage from 150MHz to 960MHz, allowing the support of all major sub-GHz ISM bands around the world.

| Region        | Center Frequency |
| ------------- | ---------------- |
| United States | 915 MHz          |
| Europe        | 433/868 MHz      |
| China         | 470/779 MHz      |

### What It Is Used For

Given its robust nature, [Verge Aero](../../) uses the long-range link for mission-critical, transmit-only data. It is used for trigger events, and for [RTCM ](../../drone-show-technology/gps-gnss/rtcm.md)data. Some examples of trigger events include:

* Launching the show
* Aborting the show (via land all or [RTH](https://wiki.droneshow.software/index.php?title=Smart_RTH\&action=edit\&redlink=1))
* Setting drone safety states
* Setting drone light modes

### Console

The long-range radio is also not absolutely necessary for a successful show. Configuration tools in the [Verge Aero Console](../../drone-show-software/verge-console/) allows all long-range data to intead be transmitted over the telemetry gateway. This alternate module has lower range, but is still sufficient for the majority of operating environments.

The long-range radio channel may be configured from the [Verge Aero Console](../../drone-show-software/verge-console/) in software by using the network configuration wizard. Total number of channels available differ by region.
