# Digit Decoder and Seven-Segment Display

[Component library](../README.md) · [Calculator](../../calculator/README.md)

## Standalone views

![Standalone decoder from the display side](../images/display-decoder-front.png)

![The same decoder from the input and wiring side](../images/display-decoder-back.png)

The purple circuitry decodes four BCD input bits into one of ten digit-selection signals, 0 through 9. The white wiring maps the selected value to the required display segments.

For example, BCD `0101` selects decimal 5, and the segment wiring enables the pattern for 5. The display uses the valid BCD digit codes 0 through 9.

## Calculator implementation

Hundreds, tens, and ones each have their own decoder and retain leading zeros. A simplified thousands driver shows 1 or stays blank. Separate signals enable fixed minus-sign and `.5` patterns.

See the [installed display circuitry](../../calculator/COMPONENTS.md#display-circuitry-in-the-assembled-calculator).

## Design credit

I used Mattbatwings' [display-design tutorial at 20:25](https://www.youtube.com/watch?v=mDLfUbAK9T0&t=1225s) as a reference for the binary-to-decimal display design.
