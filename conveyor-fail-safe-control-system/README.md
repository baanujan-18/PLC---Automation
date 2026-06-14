# Conveyor Fail-Safe Control System

## Overview

This project implements a conveyor fail-safe control system using two different control methods:

1. Hardwired relay/contactor-based control
2. Siemens S7-200 PLC-based control

The objective of the system is to stop the conveyor when specific fail-safe sensor conditions occur.

## Problem Statement

The conveyor system contains three fail-safe sensors, A, B, and C, and one emergency sensor, D.

The conveyor must stop under the following conditions:

* Sensor A and Sensor B are ON
* Sensor A and Sensor C are ON
* Emergency sensor D is ON

The stop condition can be written as:

`STOP = (A AND B) OR (A AND C) OR D`

The conveyor can run only when the stop condition is not active:

`RUN = NOT STOP`

## Input Mapping

| Sensor | Description        | PLC Input |
| ------ | ------------------ | --------- |
| A      | Fail-safe sensor A | I0.0      |
| B      | Fail-safe sensor B | I0.1      |
| C      | Fail-safe sensor C | I0.2      |
| D      | Emergency sensor   | I0.3      |

## Output Mapping

| Output | Description                         |
| ------ | ----------------------------------- |
| Q0.0   | Conveyor motor or contactor command |
| Q0.1   | Optional stop/fault indicator       |

## Truth Table

|  A |  B |  C |  D | Stop condition | Conveyor output |
| -: | -: | -: | -: | -------------: | --------------: |
|  0 |  0 |  0 |  0 |              0 |             RUN |
|  0 |  0 |  0 |  1 |              1 |            STOP |
|  0 |  0 |  1 |  0 |              0 |             RUN |
|  0 |  0 |  1 |  1 |              1 |            STOP |
|  0 |  1 |  0 |  0 |              0 |             RUN |
|  0 |  1 |  0 |  1 |              1 |            STOP |
|  0 |  1 |  1 |  0 |              0 |             RUN |
|  0 |  1 |  1 |  1 |              1 |            STOP |
|  1 |  0 |  0 |  0 |              0 |             RUN |
|  1 |  0 |  0 |  1 |              1 |            STOP |
|  1 |  0 |  1 |  0 |              1 |            STOP |
|  1 |  0 |  1 |  1 |              1 |            STOP |
|  1 |  1 |  0 |  0 |              1 |            STOP |
|  1 |  1 |  0 |  1 |              1 |            STOP |
|  1 |  1 |  1 |  0 |              1 |            STOP |
|  1 |  1 |  1 |  1 |              1 |            STOP |

## PLC Ladder Logic

The PLC program uses an internal memory bit to store the stop condition.

### Stop condition

`M0.0 = (I0.0 AND I0.1) OR (I0.0 AND I0.2) OR I0.3`

### Conveyor output

`Q0.0 = NOT M0.0`

When the stop condition is active, the conveyor output is switched OFF.

## Method 1: Hardwired Contactor-Based Control

In the first method, the logic was implemented using relay/contactor wiring. This approach is useful for understanding basic electrical control circuits and hardware interlocking.

### Advantages

* Simple for fixed logic
* No programming required
* Easy to understand physically
* Useful for learning relay and contactor control

### Limitations

* Wiring becomes complex when the logic grows
* Modifications require physical rewiring
* Troubleshooting can take more time
* Limited flexibility for future expansion

## Method 2: PLC-Based Control

In the second method, the same logic was implemented using a Siemens S7-200 PLC.

### Advantages

* Logic can be modified through software
* Reduced wiring complexity
* Easier troubleshooting
* Easier to add timers, counters, alarms, and indicators
* Suitable for future expansion
* More suitable for automation systems with changing requirements

## Hardware Used

* Conveyor training setup
* Siemens S7-200 PLC
* Fail-safe sensors
* Emergency sensor or emergency push button
* Contactor or relay interface
* Control panel
* Tower lamp indicator
* 24 V DC power supply

## Learning Outcomes

This project improved my understanding of:

* Conveyor control systems
* Fail-safe logic
* Relay and contactor-based control
* PLC ladder-logic programming
* Boolean logic implementation
* Industrial automation wiring
* Comparison between hardwired and PLC-based control

## Safety Note

This project is an educational laboratory implementation. In real industrial conveyor safety systems, certified safety relays, safety PLCs, properly rated emergency-stop circuits, and formal risk assessment are required.
