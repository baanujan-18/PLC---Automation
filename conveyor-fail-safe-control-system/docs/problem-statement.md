# Problem Statement

A conveyor control system has three fail-safe sensors A, B, and C, and one emergency sensor D.

The conveyor must stop under the following conditions:

- Sensor A and Sensor B are ON
- Sensor A and Sensor C are ON
- Emergency sensor D is ON

The stop condition is:

`STOP = (A AND B) OR (A AND C) OR D`

The conveyor can run only when the stop condition is not active:

`RUN = NOT STOP`
