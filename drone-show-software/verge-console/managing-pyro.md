# Managing Pyro

When a show is designed with pyro enabled in the Design Studio, it exports/embeds additional metadata into the flight file. When the file is opened in the console, some new buttons and UI elements are exposed. Since the pyro planning was&#x20;

## Arming/Disarming

Just like arming/disarming a drone for flight, the console supports arming/disarming the pyro modules on individual drones or the entire swarm at once. To arm all modules simultaneously, click the "Pyro" button in the show control panel. When the button is <mark style="color:red;">red</mark>, it indicates that the modules are disarmed. Clicking it will swap the state to armed.  When the button is <mark style="color:green;">green</mark> all modules are armed and clicking it will disarm all drones. When it is <mark style="color:orange;">orange</mark> some of the modules are armed and some are disarmed, with the exact number summarized as part of the button text.

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption><p>A new button appears when loading a vbake with pyro support</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption><p>Shows that the fleet is partially armed.</p></figcaption></figure>

Drones can be individually armed or disarmed by selecting the drone, navigating to the inspector panel, going to the pyro module panel, and clicking the "Arm" or "Disarm" button.

## Slotting Pyro Drones

Pyro modules leverage the [addressing system](slotting-assigning-drones.md) used for placing and assigning drones. To include a pyro drone in a show, place it into a slot that includes the same products that are mounted to the drone. To check which products are included and what cues that belong to, check the [pyro module panel](managing-pyro.md#pyro-module-info) once slotted.

To view pyro module states in the grid view, select the "Pyro View" panel at the top middle of the toolbar panel.

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption><p>Select the pyro view</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

The pyro view provides a quick way to see the status of all connected drones and whether the cues on the attached pyro modules are:

* Included in the show and connected \[<mark style="color:green;">Green</mark>]
* Included in the show and not connected or showing an error \[<mark style="color:red;">Red</mark>/<mark style="color:purple;">Magenta</mark>]
* Not included in the show \[Grey]
* Still detecting/settling \[<mark style="color:yellow;">Yellow</mark>]

If all sub-cells are green or grey, then everything is configured correctly.

## Module-States

Each pyro module provides detailed state information and fault detection/reporting. Its state is displayed in the device grid in a color-coded pattern. The cell's background color indicates if it is disarmed (<mark style="color:red;">red</mark>) , if there is a fault (<mark style="color:purple;">magneta</mark>), or if it is armed (<mark style="color:green;">green</mark>).

Additionally, state information is provided for every cue connection on the pyro module. This is represented by six smaller cells that each have a (number representing its cue ID) along with a color, (representing its state).

### Pyro Module Mode

Each pyro module provides detailed state information and fault detection/reporting. This information is displayed in the device's [inspector panel](managing-pyro.md#pyro-module-info).

| Module Mode | Description                                                                                                 |
| ----------- | ----------------------------------------------------------------------------------------------------------- |
| Idle        | The module is ready to arm or test                                                                          |
| Arming      | The module is transitioning to armed mode                                                                   |
| Armed       | The module is armed (12V enabled, fire enable is high)                                                      |
| Disarming   | The module is transitioning to idle mode                                                                    |
| Fault       | The module is in a fault state (12V disabled, fire enable is low). See the fault state for additional info. |

### Pyro Module Faults

If the drone is displaying a fault, check the info panel for more information. It may display one of the following fault labels:

| Module Fault          | Description                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------ |
| None                  | System is healthy                                                                          |
| Bad PFET              | One or more cues detected a bad PFET                                                       |
| No Power Good         | 12V power good signal was not present when expected                                        |
| Unexpected Power Good | 12V power good signal was present when not expected                                        |
| Timeout               | The client failed to issue a command within the timeout period (while not idle or faulted) |
| Comm Failure          | Hivemind failed to communicate with the pyro module                                        |
| CPU Time Error        | Hivemind is not allocating enough CPU time for the pyro module                             |
| Software Error        | There has been some unknown issue with the software                                        |

## Test-Firing a Pyro Module

For testing purposes, the console provides a method for test firing a single drone at a time. To open the test-firing panel:

1. Select a single drone
2. Navigate to the inspector
3. Navigate to the "Pyro Module" tab
4. Make sure the drone is armed and click the "Test-Fire Panel" button
5. Toggle the "Enable Test Firing" field
6. Now, click the button associated with the cue that you wish to fire

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption><p>Pyro Test-Fire Panel</p></figcaption></figure>

## Pyro Module Info

If a drone has a connected pyro module, a new tab will appear in its inspector. The "Pyro Module" tab contains all important information about the connected pyro module along with information about the pyrotechnics that expected to be mounted on it. This information appears based on where the drone is placed in the launchpad. Along with module state and cue state, each cue lists a product description along with the expected mounting direction.&#x20;

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

