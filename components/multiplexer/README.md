# Multiplexer

[Component library](../README.md) · [Calculator](../../calculator/README.md)

![Standalone multiplexer](../images/multiplexer.png)

A multiplexer selects one of two input paths according to a control signal. Repeating this selection across multiple bits allows it to select a whole binary value.

## Logic

For data inputs D0 and D1 and select S, the conventional relationship is:

`output = (NOT S AND D0) OR (S AND D1)`

| Select | Output |
| --- | --- |
| 0 | D0 |
| 1 | D1 |

D0, D1, and S describe the logical data inputs and select signal.

## Calculator implementation

Multiplexers select the first or second adder's magnitude, then choose unshifted or shifted paths for multiplication and division by 2. See the [shift stages](../../calculator/README.md#bit-shift-operations).

## Planned computer

In the [Snake computer outline](../../design/README.md#proposed-architecture), multiplexers use rectangular SELECT symbols. They choose the next program-counter value, an ALU operand, and the value written back to the register file. These symbols describe selection functions; they do not prescribe the physical Redstone layout or fix the instruction encoding.
