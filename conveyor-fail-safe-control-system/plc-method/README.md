# PLC-Based Method

This folder contains the Siemens S7-200 PLC-based implementation of the conveyor fail-safe control system.

In this method, the stopping logic is implemented using PLC ladder logic instead of hardwired relay logic. This reduces wiring complexity and makes the system easier to modify, troubleshoot, and expand.

The PLC stop condition is:

`M0.0 = (I0.0 AND I0.1) OR (I0.0 AND I0.2) OR I0.3`

The conveyor output logic is:

`Q0.0 = NOT M0.0`

## Contents

* Ladder-logic explanation
* Siemens S7-200 program file
* Ladder-logic screenshots
* PLC setup photos
* Demonstration video link
