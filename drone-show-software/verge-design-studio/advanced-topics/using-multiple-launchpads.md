# Using Multiple Launchpads

A launchpad object serves as the core to a drone show design. It is used to target shapes, transition between formations, and launch/land drones. Any number of launchpads may be placed in the scene, each with its own set of parameters and timelines. Using multiple launchpads is an excellent way to extend the runtime of a show. A new batch of drones can be launched and moved into position right before landing a previous batch to seamlessly continue a show. It is also a good way to organize/separate drones with different payloads such as pyro. All drones in the scene, regardless of launchpad, will be routed appropriately with full collision avoidance.&#x20;

## Merging Launchpads

It may be desirable to combine the drones from multiple launchpads into a single effect. This can be easily done by using a Launchpad Merger object. The merger object, when tracked by one or more launchpads, will automatically expand to contain all drones that are targeting it. For example, if two 100-drone launchpads are targeting a merger object, the merger will become a single 200-drone controller. The merger then functions exactly like a formation sequence, where other objects can be tracked and transitioned between.

When drones are added or removed from the merger, it will automatically take the transition-in or transition-out time of those drones and shift the drones already tracking the merger to their new expanded/shrunk slot counts.

<figure><img src="../../../.gitbook/assets/Merge_Launchpads.gif" alt=""><figcaption><p>Shows two 100-drone launchpads joining a single grid</p></figcaption></figure>

### Adding and Using a Launchpad Merger Object

* Right-Click on the scene view
* Choose Create > Swarm Control > Launchpad Merger
* Add track events to the launchpad merger timeline just as though it is a launchpad or a formation sequence
* Track the launchpad merger with a launchpad to join the group
* Track another object to then transition the launchpad to a different shape

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption><p>An example of the timeline for two launchpads tracking a launchpad merger (as seen in the animation above)</p></figcaption></figure>
