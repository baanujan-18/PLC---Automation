# PLC-Based Multi-Stage Metal Product Handling and Labeling System

## Overview

This project presents a PLC-based multi-stage automated metal product handling and labeling system developed using a Siemens S7-200 PLC.

The system automatically transports a metal product through three conveyor stages and performs multiple operations including:

- Product detection
- Conveyor transportation
- Timed heating
- Suction-based pick-and-place transfer
- Pneumatic positioning
- Gripper-based product handling
- Labeling-stage positioning
- Final conveyor transfer
- Automatic cycle completion

The complete process is implemented using sequential PLC ladder logic with sensors, timers, internal memory states, pneumatic actuators, suction control, a gripper, and three conveyor systems.

---

## System Architecture

The system consists of three main conveyor sections.

### Conveyor 1

Sensors:

- S1
- S2
- S3

Main operations:

- Initial metal product detection
- Conveyor transportation
- Heating process
- Product positioning for suction transfer
- Transfer of the product toward Conveyor 2

### Conveyor 2

Sensors:

- S4
- S5
- S6

Main operations:

- Receiving the product from Conveyor 1
- Product transportation
- Product positioning
- Pneumatic pick-and-place operation
- Placement at the labeling position
- Labeling dwell period
- Returning the product to Conveyor 2
- Transportation toward Conveyor 3

### Conveyor 3

Sensor:

- S7

Main operations:

- Receiving the processed product
- Final transportation
- Final product detection
- Completion of the automation cycle

---

# PLC I/O Configuration

The Siemens S7-200 PLC was configured with digital inputs and outputs for sensors, conveyors, pneumatic actuators, suction, gripper control, heating, and transfer mechanisms.

## Digital Inputs

| Symbol | PLC Address | Function |
|---|---|---|
| S1 | I0.0 | Conveyor 1 initial product detection |
| S2 | I0.1 | Conveyor 1 heating-position detection |
| S3 | I0.2 | Conveyor 1 suction-transfer position detection |
| S4 | I0.3 | Conveyor 2 receiving-position detection |
| S5 | I0.4 | Conveyor 2 pick-and-place position detection |
| S6 | I0.5 | Conveyor 2 final transfer-position detection |
| S7 | I0.6 | Conveyor 3 final product detection |
| C1S1 | I1.0 | Cylinder 1 home/backward position sensor |
| C1S2 | I1.1 | Cylinder 1 forward position sensor |
| C2S1 | I1.2 | Cylinder 2 upper position sensor |
| C2S2 | I1.3 | Cylinder 2 lower position sensor |

## Digital Outputs

| Symbol | PLC Address | Function |
|---|---|---|
| Rodless | Q0.0 | Rodless actuator control |
| TN_01 | Q0.1 | TN01 vertical transfer mechanism |
| Suction | Q0.2 | Vacuum/suction control |
| Cylinder_01 | Q0.3 | Horizontal pneumatic cylinder control |
| Cylinder_02 | Q0.4 | Vertical pneumatic cylinder control |
| Gripper | Q0.5 | Pneumatic gripper control |
| TN_02 | Q0.6 | Final product transfer/pushing mechanism |
| Conveyor_01 | Q1.0 | Conveyor 1 control |
| Conveyor_02 | Q1.2 | Conveyor 2 control |
| Conveyor_03 | Q1.4 | Conveyor 3 control |
| Heater | Q1.5 | Heating process control |

---

## I/O Summary

The control system uses:

- 11 digital inputs
- 11 digital outputs
- 7 process/product-position sensors (S1-S7)
- 4 pneumatic-cylinder position sensors
- 3 conveyor control outputs
- 2 pneumatic cylinder outputs
- 1 rodless actuator output
- 1 suction output
- 1 gripper output
- 2 transfer mechanism outputs (TN01 and TN02)
- 1 heater output

The sensor inputs provide feedback to the PLC so that the controller can determine when each physical stage has been completed.

The PLC outputs control the conveyors, pneumatic mechanisms, suction system, gripper, heater, and product-transfer mechanisms.

---

# Automated Process Sequence

## Stage 1 - Initial Product Detection

A metal product is placed at the beginning of Conveyor 1.

Sensor S1 detects the product.

The PLC waits for:

**2 seconds**

After the delay is completed:

**Conveyor 1 starts.**

The product begins moving toward S2.

---

## Stage 2 - Heating Process

The product travels along Conveyor 1 until S2 detects it.

When S2 is activated:

**Conveyor 1 stops.**

The heating process starts.

The product remains at the heating stage for:

**5 seconds**

After the heating period:

- Heater switches OFF
- Conveyor 1 starts again

The metal product continues toward S3.

---

## Stage 3 - Suction Transfer Preparation

When S3 detects the product:

**Conveyor 1 stops.**

The suction-transfer sequence begins.

The system waits according to the programmed sequence and the rodless actuator moves forward toward Conveyor 1.

The rodless mechanism positions the suction assembly above the metal product.

---

## Stage 4 - TN01 and Suction Pick-Up

TN01 moves downward toward the product.

After the required timed sequence, the suction mechanism switches ON.

The suction mechanism holds the metal product.

TN01 then moves upward.

The product is now lifted from Conveyor 1.

---

## Stage 5 - Transfer from Conveyor 1 to Conveyor 2

After lifting the product, the rodless actuator moves backward toward Conveyor 2.

The product is transported horizontally from the Conveyor 1 position toward the Conveyor 2 position.

TN01 then moves downward.

The suction mechanism switches OFF.

The metal product is released onto the Conveyor 2 starting area near S4.

TN01 then returns upward.

The transfer mechanism is now ready for the next cycle.

---

## Stage 6 - Conveyor 2 Transportation

After the metal product has been placed onto Conveyor 2:

**Conveyor 2 starts.**

The product travels toward S5.

When S5 detects the product, the conveyor is not stopped immediately.

A positioning delay of:

**0.4 seconds**

is used.

This allows the metal product to move slightly beyond the S5 detection point and reach the correct physical position underneath the pneumatic pick-and-place mechanism.

After the positioning delay:

**Conveyor 2 stops.**

---

# Pneumatic Pick-and-Place System

The pick-and-place section uses two pneumatic cylinders and a gripper.

### Cylinder 1

Cylinder 1 provides horizontal movement.

Position feedback:

- C1S1 = Home/backward position
- C1S2 = Forward position

### Cylinder 2

Cylinder 2 provides vertical movement.

Position feedback:

- C2S1 = Upper position
- C2S2 = Lower position

### Normal/Home Position

The normal mechanical condition is:

- Cylinder 1 at backward/home position
- Cylinder 2 at upper position

Therefore:

- C1S1 confirms Cylinder 1 home position
- C2S1 confirms Cylinder 2 upper position

The PLC uses these sensors to confirm the mechanism position before continuing the sequence.

---

## Stage 7 - Product Pick-Up from Conveyor 2

The PLC first confirms the required cylinder positions.

Cylinder 2 moves downward toward the metal product.

The PLC checks C2S2 to confirm that Cylinder 2 has reached its lower position.

The gripper then closes and grips the metal product.

The system waits for the programmed sequence delay.

Cylinder 2 moves upward.

The PLC checks C2S1 to confirm the upper position.

The product has now been lifted from Conveyor 2.

---

## Stage 8 - Movement Toward Labeling Position

Cylinder 1 moves horizontally forward toward the labeling position.

The PLC checks C1S2 to confirm that Cylinder 1 has reached the forward position.

Cylinder 2 then moves downward.

C2S2 confirms that Cylinder 2 has reached the lower position.

The gripper opens.

The metal product is released at the labeling position.

---

## Stage 9 - Labeling Process

After releasing the product:

Cylinder 2 moves upward.

The PLC checks C2S1 to confirm the upper position.

The system then provides:

**5 seconds**

for the labeling process.

During this period, the product remains at the labeling position.

---

## Stage 10 - Product Pick-Up After Labeling

After the labeling period is completed:

Cylinder 2 moves downward again.

C2S2 confirms the lower position.

The gripper closes and grips the labeled metal product.

After the programmed delay:

Cylinder 2 moves upward.

C2S1 confirms the upper position.

---

## Stage 11 - Return Toward Conveyor 2

Cylinder 1 moves backward toward its original/home position.

C1S1 confirms that Cylinder 1 has reached the home position.

Cylinder 2 then moves downward.

C2S2 confirms the lower position.

The gripper opens.

The processed metal product is released back onto Conveyor 2.

After the product is released, Cylinder 2 moves upward again.

C2S1 confirms the upper position.

The pick-and-place sequence is now complete.

---

## Stage 12 - Conveyor 2 Restart

After the product has been returned to Conveyor 2:

**Conveyor 2 starts again.**

The product travels toward S6.

When S6 detects the product, the PLC performs the programmed final positioning sequence.

A short positioning delay of:

**0.1 seconds**

is used.

After this delay:

**Conveyor 2 stops.**

---

## Stage 13 - Transfer to Conveyor 3

After Conveyor 2 stops, the final transfer sequence begins.

Conveyor 3 starts.

TN02 operates as the final transfer/pushing mechanism.

TN02 pushes/transfers the metal product from the Conveyor 2 section toward Conveyor 3.

The metal product then continues along Conveyor 3.

---

## Stage 14 - Final Product Detection

The metal product travels along Conveyor 3 until it reaches S7.

When S7 detects the product:

- The final product position is confirmed
- The current automation cycle is completed
- The PLC sequence returns to its initial state

The system is then ready for the next metal product.

---

# Overall Process Flow

The complete process can be summarized as:

Metal Product Entry

↓

S1 Detection

↓

2-Second Delay

↓

Conveyor 1

↓

S2 Detection

↓

Heating Process

↓

Conveyor 1 Restart

↓

S3 Detection

↓

Rodless + TN01 + Suction Transfer

↓

Product Placed on Conveyor 2

↓

Conveyor 2

↓

S5 Detection and Positioning

↓

Pneumatic Pick-and-Place

↓

Product Placed at Labeling Position

↓

Labeling Period

↓

Product Picked Again

↓

Product Returned to Conveyor 2

↓

Conveyor 2 Restart

↓

S6 Detection

↓

TN02 Transfer

↓

Conveyor 3

↓

S7 Final Detection

↓

Cycle Complete

---

# Timing Strategy

Timers are an important part of the sequential control system.

The main programmed timing periods include:

| Timing | Purpose |
|---|---|
| 2 seconds | Main sequential actuator and process delays |
| 5 seconds | Heating process |
| 0.4 seconds | Product positioning after S5 detection |
| 5 seconds | Labeling process |
| 0.1 seconds | Product positioning around the S6 transfer stage |

The 2-second delays are used throughout the sequential operation where required to allow sufficient time for mechanical movements and process transitions.

---

# PLC Control Strategy

The project uses sequential PLC control rather than only simple Boolean ON/OFF logic.

The PLC program uses:

- Digital sensor inputs
- Digital outputs
- Internal memory bits
- Timers
- SET operations
- RESET operations
- Position feedback
- Sequential state transitions

Internal memory states are used to represent the different stages of the machine cycle.

A stage is activated only when the required previous operation has been completed.

For pneumatic movements, position sensors are used to confirm that the actuator has reached the required position before the PLC proceeds to the next stage.

This creates a sequence such as:

Command Actuator

↓

Wait for Movement

↓

Check Position Sensor

↓

Position Confirmed

↓

Continue to Next Stage

This approach provides more reliable sequential operation than controlling the complete process only using fixed time delays.

---

# Main Hardware and Control Elements

The system includes:

- Siemens S7-200 PLC
- Three conveyor systems
- Seven process-position sensors (S1-S7)
- Rodless transfer actuator
- TN01 vertical transfer mechanism
- TN02 final transfer/pushing mechanism
- Vacuum/suction handling mechanism
- Horizontal pneumatic cylinder (Cylinder 1)
- Vertical pneumatic cylinder (Cylinder 2)
- Pneumatic gripper
- Four cylinder position sensors
- Heating mechanism
- Pneumatic solenoid valves
- Compressed-air supply
- PLC digital input/output interfacing

---

# Key Automation Concepts Demonstrated

This project demonstrates several important industrial automation concepts:

- Multi-stage process automation
- PLC-based sequential control
- Conveyor synchronization
- Sensor-based product tracking
- Timer-based sequencing
- Pneumatic actuator control
- Position feedback
- Pick-and-place automation
- Vacuum material handling
- Pneumatic gripping
- Product positioning
- Multi-conveyor material transfer
- SET/RESET ladder programming
- PLC internal memory-state control
- Automatic cycle reset

---

# Learning Outcomes

Through this project, practical experience was gained in:

- Siemens S7-200 PLC programming
- PLC ladder logic development
- Industrial sensor interfacing
- PLC timers
- Internal PLC memory bits
- SET and RESET instructions
- Sequential machine control
- Pneumatic cylinder operation
- Solenoid valve control
- Cylinder position feedback
- Suction-based material handling
- Pneumatic gripper operation
- Conveyor control
- Multi-conveyor synchronization
- Pick-and-place sequence development
- Product positioning
- Industrial automation troubleshooting
- Testing complete automated sequences

---

# Repository Structure

```text
plc-multi-stage-metal-product-handling-labeling-system/
│
├── README.md
│
├── plc-program/
│   ├── ladder-diagram.pdf
│   └── ladder-logic-screenshot.png
│
├── hardware/
│   ├── complete-system.jpg
│   ├── conveyor-1.jpg
│   ├── suction-transfer-system.jpg
│   ├── conveyor-2-labeling-station.jpg
│   ├── pneumatic-pick-and-place.jpg
│   └── conveyor-3-final-transfer.jpg
│
├── media/
│   └── demo-video-link.md
│
└── colab/
    └── process-sequence-verification.ipynb
