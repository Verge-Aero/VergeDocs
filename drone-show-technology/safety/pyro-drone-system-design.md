---
hidden: true
---

# Pyro Drone System Design

## The Safety Benefits of an Integrated System

### Failure State Handling

Independent systems fail independently. With pyro on drones, that statement is catastrophic. As the table below shows, mutual failure of systems is necessary to mitigate safety risks. Independent systems require fast-paced manual human intervention. It’s a recipe for safety risks to go unmitigated.

<table data-header-hidden><thead><tr><th></th><th width="147"></th><th></th><th></th><th width="150"></th></tr></thead><tbody><tr><td>Failure Mode</td><td>Independent Result</td><td>Independent Mitigition</td><td><p>Integrated</p><p>Result</p></td><td><p>Integrated</p><p>Mitigition</p></td></tr><tr><td>Drone Power Failure</td><td>Drone begins plummeting. Firing is system still active.</td><td>Operator must disable pyro module before or after impact. Damage to pyro module while still active may lead to undesirable results.</td><td>Firing system turns off. Drone is disabled.</td><td>None necessary</td></tr><tr><td>Pyro Power Failure</td><td>Firing system is disabled. Drone continues show safely.</td><td>None necessary</td><td>Firing system is disabled. Drone continues show safely.</td><td>None necessary</td></tr><tr><td>Drone Comms Loss</td><td>Firing operator may continue to monitor system state for arm/disarm.</td><td>Operator must discover and disable associated pyro module asset as a drone comms failure requires it.1</td><td>Drone detects loss of heartbeats from GCS and internally disables the firing module.</td><td>None necessary</td></tr><tr><td>Pyro Comms Loss</td><td>No ability to arm or disarm pyro module remotely. </td><td>No possible mitigation. With no path to the pyro module it cannot be armed or disarmed automatically or manually while in flight.2</td><td>Module can no longer be fired. It is disabled by virtue of no comms to the drone.</td><td>None necessary</td></tr><tr><td>Drone Failsafe</td><td>Drone autolands or returns to home. Firing module continues to be active.</td><td>Operator must disable pyro module before it lands or it returns to the launchpad such that it doesn’t fire improperly. </td><td>Firing module is automatically disabled</td><td>None necessary</td></tr><tr><td>Drone Doesn’t Launch</td><td>Module continues to be armed.</td><td>Operator must disable pyro module manually before it fires.</td><td>Firing module is never armed</td><td>None necessary</td></tr></tbody></table>

1 A well-behaving light-show drone failsafes automatically upon GCS link-loss, so the operator MUST disable that drone's pyro, or all pyro, to ensure ignition does not occur as the drone is failsafing. The additional complexity of identifying the drone and mapping it to an associated firing module is extremely difficult to do in a time-sensitive manner. Functionally, the only mitigation is to disable all firing modules.

2 As an example of module behavior, modern versions of firmware for the Cobra wireless firing module have a very long auto-disarm time. If communication is lost, by either going out of range, or if the firing remote dies, the module will not disarm itself for upwards of 60 seconds. [See reference here](https://help.cobrafiringsystems.com/hc/en-us/articles/5495286986907-If-I-power-off-my-18R2-will-my-modules-stop-firing).
