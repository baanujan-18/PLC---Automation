# Hardwired Contactor-Based Method

This folder contains the hardwired relay/contactor-based implementation of the conveyor fail-safe control system.

In this method, the stopping logic is implemented using physical wiring, contactors, and relay-based control. This approach is useful for understanding traditional industrial control wiring and hardware interlocking.

The conveyor stops when:

`STOP = (A AND B) OR (A AND C) OR D`

The conveyor runs only when the stop condition is not active:

`RUN = NOT STOP`

## Contents

* Contactor logic explanation
* Wiring diagram
* Control-panel photos
* Hardwired setup photos
* Demonstration video link
