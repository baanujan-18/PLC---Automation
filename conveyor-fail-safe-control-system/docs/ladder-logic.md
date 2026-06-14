# Ladder Logic

## Input Mapping

| Sensor | PLC Input |
|---|---|
| A | I0.0 |
| B | I0.1 |
| C | I0.2 |
| D | I0.3 |

## Output Mapping

| Output | Description |
|---|---|
| Q0.0 | Conveyor motor command |
| Q0.1 | Optional stop/fault indicator |

## Stop Logic

The stop condition is stored in internal memory bit M0.0.

`M0.0 = (I0.0 AND I0.1) OR (I0.0 AND I0.2) OR I0.3`

## Conveyor Output Logic

`Q0.0 = NOT M0.0`

When M0.0 is ON, the conveyor output turns OFF.
