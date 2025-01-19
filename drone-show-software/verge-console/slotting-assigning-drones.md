# Slotting - Assigning Drones

Most of the work that goes into setting up a drone show goes into laying out the launchpad and assigning roles to each drone. The act of assigning a drone is known as _slotting_.&#x20;

When a flyable show is generated via the [Verge Web Portal](../verge-web-portal/) and loaded into the console, geo-locked coordinates, or _slots,_ are created which correspond to the starting positions of each drone. One drone must be placed in each slot in the real world so that it can be assigned to it.

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-26 115910 (1).png" alt=""><figcaption></figcaption></figure>

## Launchpad Overview

The slotting panel contains a short summary of launchpad characteristics that simplify setup. Launchpad Dimensions and Launchpad Density are displayed in Meters (if Metric units are selected) or Feet (if Imperial units are selected).

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-26 121332.png" alt=""><figcaption></figcaption></figure>

## Slotting Solvers

There are two available solvers for assignment. Each solver assigns drones to slot in a unique way and will provide different results. If drones are placed _perfectly_ in launchpad positions and GPS quality is optimal, then the same solution will be provided by all methods.

### Legacy

This is the solver that has been in use since the original release of the Console application. Slots are assigned with a simple algorithm that finds the closest slot to a drone and then conversely chooses the drone _closest_ to that slot (only if it also meets certain system health requirements). There is no global optimization method and is also problematic in the case where two drones are closest to one slot. In this case, one drone will be left unassigned.

### Smart Slotting

This is the latest, and preferred, method. This option was introduced in Console version 2024.2. The _Smart Slotting_ solver considers the state of the entire fleet and compares it to the launchpad. It applies multiple constraints, such as distance limits, and seeks to minimize the total distance from all drones to the slots in the launchpad. This overcomes weaknesses in the previous methodology, supporting less structured launchpad layouts and cases where GPS accuracy is sub-optimal.

## Slotting Modes

### Continuous

The default option, continuous slotting will automatically solve, assign, and slot drones at regular intervals. This mode is hands-off and allows pilots to focus on placing drones in the field. Simply power on drones, place them, and the console will do the rest.

### Static

This option disables automatic slotting, but provides a number of input options to manage when and how slotting occurs. This mode also causes a new set of buttons to appear in the drone inspector window.
