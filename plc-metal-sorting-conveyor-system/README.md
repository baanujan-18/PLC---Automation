# PLC-Based Metal Sorting Conveyor with Pneumatic Ejection

## Overview

This project implements an automated metal-sorting conveyor system using a Siemens S7-200 PLC, two photoelectric sensors, one inductive proximity sensor, a pneumatic actuator, and three status indicators.

The system detects an object at the beginning of the conveyor, starts the conveyor after a timed delay, identifies whether the object is metallic, and separates metallic objects using a pneumatic actuator.

Non-metallic objects continue to the end of the conveyor and are detected by the final photoelectric sensor.

## System Components

* Siemens S7-200 PLC
* Conveyor motor
* D1 photoelectric sensor
* D2 inductive proximity sensor
* D3 photoelectric sensor
* Pneumatic actuator
* Solenoid valve
* Green status indicator
* Orange status indicator
* Red status indicator
* 24 V DC power supply
* PLC control panel

## Sensor Functions

| Sensor | Type                       | PLC Address | Function                                         |
| ------ | -------------------------- | ----------- | ------------------------------------------------ |
| D1     | Photoelectric sensor       | I0.0        | Detects an object at the conveyor entry          |
| D2     | Inductive proximity sensor | I0.1        | Detects metallic objects                         |
| D3     | Photoelectric sensor       | I0.2        | Detects non-metallic objects at the conveyor end |

## Output Mapping

| Output             | PLC Address | Function                                       |
| ------------------ | ----------- | ---------------------------------------------- |
| Conveyor motor     | Q0.1        | Runs the conveyor                              |
| Green lamp         | Q0.2        | Indicates that the conveyor is running         |
| Orange lamp        | Q0.3        | Indicates the metal-ejection process           |
| Red lamp           | Q0.4        | Indicates that the conveyor is stopped         |
| Pneumatic actuator | Q0.5        | Pushes metallic objects away from the conveyor |

## Sequence of Operation

### 1. Initial object detection

An object is placed at the beginning of the conveyor.

When the D1 photoelectric sensor detects the object, timer T37 starts.

After a 2-second delay, the PLC switches ON the conveyor motor.

The green indicator switches ON while the conveyor is running, and the red indicator switches OFF.

### 2. Metal-object sequence

When a metallic object reaches the D2 inductive proximity sensor:

1. D2 detects the metal object.
2. The conveyor stops immediately.
3. The green indicator switches OFF.
4. The red indicator switches ON.
5. The orange indicator switches ON.
6. Timer T38 provides a 2-second delay.
7. The pneumatic actuator switches ON.
8. The actuator pushes the metallic object away from the conveyor.
9. Timer T39 keeps the actuator active for 2 seconds.
10. The actuator switches OFF and returns automatically.
11. The orange indicator switches OFF.
12. The system returns to the initial waiting condition.

### 3. Non-metal-object sequence

If D2 does not detect the object, the object is considered non-metallic.

The conveyor continues moving until the object reaches D3.

When D3 detects the object:

1. The conveyor stops.
2. The green indicator switches OFF.
3. The red indicator switches ON.
4. The object is manually removed.
5. The next operating cycle begins when a new object is placed at D1.

## Status Indicators

| System condition                | Green | Orange | Red |
| ------------------------------- | ----: | -----: | --: |
| Conveyor stopped                |   OFF |    OFF |  ON |
| Initial 2-second delay          |   OFF |    OFF |  ON |
| Conveyor running                |    ON |    OFF | OFF |
| Metal detected                  |   OFF |     ON |  ON |
| Actuator operating              |   OFF |     ON |  ON |
| Non-metal object detected at D3 |   OFF |    OFF |  ON |

## PLC Timer Functions

| Timer |  Duration | Function                                             |
| ----- | --------: | ---------------------------------------------------- |
| T37   | 2 seconds | Delay between D1 detection and conveyor start        |
| T38   | 2 seconds | Delay between metal detection and actuator operation |
| T39   | 2 seconds | Actuator operating duration                          |

## Ladder-Logic Summary

The PLC program performs the following operations:

* D1 starts timer T37.
* T37 sets the conveyor output Q0.1.
* D2 resets the conveyor, sets internal memory M0.0, and switches ON the orange indicator.
* M0.0 starts timer T38.
* T38 switches ON the pneumatic actuator and starts timer T39.
* T39 resets the actuator, internal memory, and orange indicator.
* D3 resets the conveyor output.
* Q0.1 directly controls the green indicator.
* The normally closed condition of Q0.1 controls the red indicator.

## Project Results

The system successfully separates metallic objects from non-metallic objects.

Metallic objects are detected by the inductive proximity sensor and removed using the pneumatic actuator. Non-metallic objects pass the metal-detection point and continue until they are detected at the end of the conveyor.

## Learning Outcomes

This project improved my understanding of:

* Siemens S7-200 PLC programming
* Sequential ladder logic
* Timer-based automation
* Photoelectric sensor interfacing
* Inductive proximity sensor interfacing
* Pneumatic actuator control
* Metal and non-metal object classification
* Conveyor control
* Industrial status indication
* PLC input and output mapping

## Safety Note

This project was developed as an educational laboratory implementation. Industrial conveyor and pneumatic systems require proper guarding, emergency-stop circuits, electrical protection, pneumatic isolation, and formal risk assessment.
