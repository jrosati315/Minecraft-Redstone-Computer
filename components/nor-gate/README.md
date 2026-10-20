# NOR Gate

[Component library](../README.md) · [Project overview](../../README.md)

A NOR gate outputs 1 only when both inputs are 0. Its output is the inverse of OR.

![Standalone nor gate](../images/nor-gate.png)

The central circuit appears to be a NOR gate: the two inputs join before the output is inverted.

## Logic

`output = NOT (A OR B)`

| A | B | Output |
| --- | --- | --- |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

Here, 1 means powered and 0 means unpowered.
