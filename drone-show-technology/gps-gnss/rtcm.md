# RTCM

RTCM (Radio Technical Commission for Maritime) is a protocol that supports transferring a variety of correction messages from a base station to a rover (or in our case a drone). In an [RTK](rtk-gps.md)-enabled [GNSS](https://wiki.droneshow.software/index.php?title=GNSS\&action=edit\&redlink=1) system, RTCM data must be regularly generated/transmitted by the base station and received by the rover to attain cm-level accuracy. Data is sent at roughly 1 Hz, or once per second. If an RTCM stream is lost, [GNSS](https://wiki.droneshow.software/index.php?title=GNSS\&action=edit\&redlink=1) accuracy will degrade until standard 3D-Fix is reached (\~3 meters). This is well beyond the inter-drone distance used during show design, so a loss of RTCM can result in collisions.

If you've ever seen a drone show look "fuzzy" or chaotic, then it is most likely due to a loss of RTCM.

### Data Transfer

In Verge Aero's system, RTCM data is transmitted via [LoRa](../../drone-show-hardware/networking/lora-gateway.md) radio. As this is the only data stream that is absolutely necessary during an active drone show, [LoRa](../../drone-show-hardware/networking/lora-gateway.md) maximizes the likelihood of successful reception. RTCM data is _also_ optionally sent over the primary gateway, however it requires that a [Verge Aero Console](../../drone-show-software/verge-console/) be connected and active. Having multiple radio paths improves the system's robustness.
