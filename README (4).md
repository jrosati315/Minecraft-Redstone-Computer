# Full Adder

[Component library](../README.md) · [Ripple-carry adder](../ripple-carry-adder/README.md)

A full adder adds two one-bit inputs and a carry-in, producing a sum bit and carry-out. Connecting each carry-out to the next stage builds a wider adder.

![Standalone full adder inside an orange border](../images/full-adder.png)

This is my standalone full-adder example.

## Logic

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
