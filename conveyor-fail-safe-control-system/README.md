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
