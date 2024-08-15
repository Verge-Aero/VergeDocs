# RTK GPS

Real-time kinematic positioning (RTK) is an enhancement to standard [GNSS](https://wiki.droneshow.software/index.php?title=GNSS\&action=edit\&redlink=1) that provides realtime corrections for errors in GPS signals. A standard RTK setup consists of a fixed, unmoving base station which collects and resolves GPS errors. It then embeds the corrections inside of a data packet, such as [RTCM](https://wiki.droneshow.software/wiki/RTCM), and is transmitted to a rover which can move freely, such as a drone. Standard GPS 3D-Fix resolves to an accuracy of around 3 meters while a proper RTK setup will provide accuracy down to 1-2 centimeters. This is the core technology that allows outdoor drone shows to maintain their precision and tight formations.

### RTK Modes

RTK correction does not guarantee centimeter-level precision. It requires favorable conditions, optimal positioning, and a line-of-sight setup with the rovers to obtain the best resolve. There are two observable RTK quality states:

* RTK Float
  * RTK is active, however the accuracy is not optimal
  * Accuracies range from 1.5 meters to \~3 cm
  * RTK float may still be optimal enough for a successful flight, especially close to the
* RTK Fix
  * RTK is in an optimal state
  * Accuracy is at or below 2 cm

It is also possible to be in neither RTK states and merely be in a DGPS state. DGPS (Differential GPS) is a lesser performing version of RTK. In this state, the drone is unable to perform in a drone show properly.

### Best Practices

The rules for setting up an RTK base station are essentially the same as those for any GPS device.

* Always try to have the clearest view of the sky possible
* Raise the antenna up as high as possible without compromising stability
* Avoid placement next to buildings or other flat surfaces that can introduce multi-pathing
* Avoid placing below tree coverage. Tree canopies have been found to have a significant detrimental impact on RTK quality

#### Additional Info

* Satellites are in constant motion and the satellites available may vary significantly throughout the day
* Cloud coverage _can_ have an impact on accuracy
* The base station can only transmit RTK data for satellites that have an unobstructed view to its antenna. Drones, once in the air, will generally have a completely clear view of the sky and will receive data from all available satellites. A poorly placed RTK antenna, such as one placed next to trees or buildings, will be the limiting factor in these cases.
* Solar Storms can have a very large negative impact on RTK accuracy. You should always refer to the NOAA website for updates on active or upcoming storms: [Space Weather Prediction Center](https://www.swpc.noaa.gov/)
