---
hidden: true
---

# VRSP

The **V**erge **R**obotics **S**treaming **P**rotocol is a real-time network protocol that is designed to enable third-party applications to display the active state of a Verge Design Studio session.

The protocol supports any&#x20;

All VRSP packets start with a standard header:

`Packet Identifier:` A string starting with "VRSP\_" followed by a packet identifier

`Version:` A byte that indicates the protocol's version \[Currently always 1]

`Instance ID:` An unsigned integer that identifies

## Definition Packet - `"VRSP_DEF"`

Definition packets are responsible for providing static information about an active swarm. Before any data packets are parsed, at least one definition packet with matching instance ID must be received. Definition packets are sent out at a reduced rate (Default: 1 Hz) such that&#x20;

Definition packets&#x20;

A definition packet consists of the following information:



### Payload Definitions

### Device Definition Table

## Data Packet
