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

These are logical labels. The physical paths and select polarity in this screenshot still need to be labeled.

## Calculator implementation

Multiplexers select the first or second adder's magnitude, then choose unshifted or shifted paths for multiplication and division by 2. See the [shift stages](../../calculator/README.md#bit-shift-operations).

## Details to document

- Data inputs, select signal, and output in the standalone view
- Close-up of the installed shift multiplexers
- Design source for this layout
