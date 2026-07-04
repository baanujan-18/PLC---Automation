# PLC-Based Knight Rider LED Pattern

## Overview

This project implements a Knight Rider-style LED sequence using a Siemens S7-200 PLC and eight digital outputs.

Eight LEDs were connected to PLC outputs Q0.0 through Q0.7. The PLC program activates the LEDs one at a time, moving the illuminated position from the first LED to the last LED and then returning in the opposite direction.

The sequence repeats continuously:

`Q0.0 → Q0.1 → Q0.2 → Q0.3 → Q0.4 → Q0.5 → Q0.6 → Q0.7 → Q0.6 → Q0.5 → Q0.4 → Q0.3 → Q0.2 → Q0.1 → Repeat`

## Project Objective

The objective of this project was to understand and practically test:

* Sequential PLC output control
* PLC timer operation
* PLC counter operation
* Set and reset instructions
* Repeating forward and reverse sequences
* Physical connection of LEDs to PLC digital outputs

## Hardware Used

* Siemens S7-200 PLC
* Eight LEDs
* Current-limiting resistors
* Connecting wires
* PLC power supply
* Programming computer
* STEP 7 Micro/WIN software

## PLC Output Mapping

| PLC Output | Connected Device |
| ---------- | ---------------- |
| Q0.0       | LED 1            |
| Q0.1       | LED 2            |
| Q0.2       | LED 3            |
| Q0.3       | LED 4            |
| Q0.4       | LED 5            |
| Q0.5       | LED 6            |
| Q0.6       | LED 7            |
| Q0.7       | LED 8            |

## Program Operation

The ladder program uses timer T37 to generate the timing signal for the LED sequence.

Counters C0 through C13 represent the individual stages of the Knight Rider pattern.

Each counter stage performs two main operations:

1. Resets the eight PLC outputs beginning from Q0.0.
2. Sets the required output for the current sequence position.

The first eight output stages create the forward movement:

`Q0.0 → Q0.1 → Q0.2 → Q0.3 → Q0.4 → Q0.5 → Q0.6 → Q0.7`

The remaining stages create the reverse movement:

`Q0.6 → Q0.5 → Q0.4 → Q0.3 → Q0.2 → Q0.1`

At the end of the sequence, the counters are reset and the pattern starts again.

## Ladder-Logic Structure

* Network 1: Timing pulse generation using T37
* Networks 2–15: Sequence stages using counters C0 to C13
* Networks 16–23: Forward LED sequence from Q0.0 to Q0.7
* Networks 24–29: Reverse LED sequence from Q0.6 to Q0.1
* Final network: Counter reset and automatic sequence repetition

## Physical Implementation

Eight LEDs were connected to the Siemens S7-200 PLC outputs Q0.0 through Q0.7.

After downloading the ladder program to the PLC, the outputs were monitored and tested physically. The LEDs illuminated one at a time, moved from one side to the other, and then returned in the reverse direction.

This physical test confirmed that the timer, counters, set/reset instructions, and output sequence operated correctly.

## Repository Contents

```text
plc-program/  Original Siemens ladder diagram and clean documentation PDF
colab/        Colab notebook used to generate the ladder documentation
photos/       PLC setup, LED wiring, and testing photographs
media/        Demonstration-video link
```

## Demonstration

The project demonstration video shows:

* The Siemens S7-200 PLC setup
* Eight LEDs connected to outputs Q0.0 through Q0.7
* Forward LED movement
* Reverse LED movement
* Continuous repetition of the Knight Rider pattern

The demonstration-video link is available in:

`media/demo-video-link.md`

## Learning Outcomes

This project improved my understanding of:

* Siemens S7-200 PLC programming
* Timer and counter instructions
* Sequential control
* Set and reset operations
* PLC digital output wiring
* Forward and reverse output patterns
* Practical testing of ladder logic
* PLC program documentation using Google Colab

## Note

The original Siemens STEP 7 Micro/WIN ladder program is the executable PLC program.

The Colab notebook and generated ladder PDF are included only for documentation and GitHub presentation.
