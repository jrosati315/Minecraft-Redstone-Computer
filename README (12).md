# Ripple-Carry Adders

[Component library](../README.md) · [Calculator](../../calculator/README.md)

## Eight-bit standalone adder

![Standalone eight-bit ripple-carry adder](../images/eight-bit-adder.png)

This adder adds two eight-bit numbers. Each of its eight positions receives one bit from A and one from B, then passes its carry to the next position. The final carry-out can extend the answer to nine bits.

The paired input indicators sit along the lower edge and the eight sum indicators along the upper edge.

## Four-bit standalone example

![Standalone four-bit ripple-carry adder](../images/four-bit-adder.png)

This is a separate four-bit version of the ripple-carry adder. Each bit's carry-out feeds the next more significant bit's carry-in. The calculator uses two ripple-carry adders with eight-bit input values.

## Logic

Each full-adder stage follows these relationships:

`sum = A XOR B XOR carry_in`

`carry_out = (A AND B) OR (carry_in AND (A XOR B))`

| A | B | Carry-in | Sum | Carry-out |
| --- | --- | --- | --- | --- |
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 0 | 1 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |

## Calculator implementation

The first adder handles addition or two's-complement subtraction. The second converts negative subtraction results into positive magnitudes. See the [installed arithmetic stage](../../calculator/COMPONENTS.md#two-adder-arithmetic-stage-in-the-calculator).
