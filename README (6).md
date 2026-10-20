# Multiplexer

[Component library](../README.md) · [Calculator](../../calculator/README.md)

![Standalone multiplexer](../images/multiplexer.png)

This multiplexer uses a control signal to choose between two input paths. Repeating the circuit for each bit lets it select a whole binary value.

## Logic

With data inputs D0 and D1 and select signal S:

`output = (NOT S AND D0) OR (S AND D1)`

| Select | Output |
| --- | --- |
| 0 | D0 |
| 1 | D1 |

D0, D1, and S describe the logical data inputs and select signal.

## Calculator implementation

Multiplexers select the first or second adder's magnitude, then choose unshifted or shifted paths for multiplication and division by 2. See the [shift stages](../../calculator/README.md#bit-shift-operations).

## Planned computer

In the [Snake computer outline](../../design/README.md#proposed-architecture), multiplexers use rectangular SELECT symbols. They choose the next program-counter value, an ALU operand, and the value written back to the register file. The symbols show which values can be selected. The Redstone layout and instruction encoding are still being designed.
