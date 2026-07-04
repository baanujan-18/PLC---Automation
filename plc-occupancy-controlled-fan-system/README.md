# PLC-Based Occupancy-Controlled Fan System

## Overview

This project implements an automatic fan-control system using a programmable logic controller and occupancy counting.

Two push buttons were used to simulate entry and exit sensors. The PLC counts the number of people entering and leaving and switches three fans according to the current occupancy.

## Operating Conditions

| Number of people | Fan 1 | Fan 2 | Fan 3 |
| ---------------: | ----: | ----: | ----: |
|                0 |   OFF |   OFF |   OFF |
|              1–4 |    ON |   OFF |   OFF |
|              5–8 |    ON |    ON |   OFF |
|        9 or more |    ON |    ON |    ON |

## PLC Input Mapping

| Input | Address | Function                                   |
| ----- | ------- | ------------------------------------------ |
| S1    | I0.0    | Simulated entry sensor and count-up input  |
| S2    | I0.1    | Simulated exit sensor and count-down input |

## PLC Output Mapping

| Output | Address | Function                              |
| ------ | ------- | ------------------------------------- |
| Fan 1  | Q0.0    | Operates when occupancy is at least 1 |
| Fan 2  | Q0.1    | Operates when occupancy is at least 5 |
| Fan 3  | Q0.2    | Operates when occupancy is at least 9 |

## PLC Logic

Three up/down counters were used with preset values of 1, 5, and 9.

* Counter C0 controls Fan 1.
* Counter C1 controls Fan 2.
* Counter C2 controls Fan 3.
* The entry input increments all counters.
* The exit input decrements all counters.

This allows the fan stages to switch automatically as occupancy increases or decreases.

## Electrical Setup

A 230 V AC supply was converted to 24 V DC using a DC power supply for the PLC and control circuit.

A relay module was used between the PLC outputs and the fan circuits. This provided output interfacing and electrical isolation between the PLC control side and the fan loads.

## Hardware Used

* Programmable logic controller
* Two push buttons representing entry and exit sensors
* Three fans
* Relay interface module
* 230 V AC to 24 V DC power supply
* Connecting wires
* Control terminals

## Learning Outcomes

This project improved my understanding of:

* PLC up/down counters
* Occupancy-based automation
* Multi-stage fan control
* PLC input and output mapping
* Relay interfacing
* Power-supply integration
* Ladder-logic design
* Hardware wiring and testing

## Safety Note

The project was completed as a laboratory implementation. Mains-voltage wiring must use properly rated relays, protective devices, insulation, grounding, and safe electrical working procedures.

