# Calculator Component Gallery

[Project overview](README.md) · [Calculator description](CALCULATOR.md)

These screenshots show standalone component examples and circuitry inside the assembled calculator. They document the build's structure; example input/output tests can be added alongside them as they are recorded.

## Standalone four-bit ripple-carry adder

![Standalone four-bit adder built from orange blocks](images/four-bit-adder.png)

This four-bit example shows the ripple-carry adder design used in the calculator. The carry from each bit feeds the next more significant bit. The standalone example illustrates the component; the calculator itself accepts two eight-bit inputs.

## Standalone multiplexer

![Standalone multiplexer with colored input paths and control wiring](images/multiplexer.png)

A multiplexer selects one of two input paths according to a control signal. The calculator uses multiplexers to select the appropriate arithmetic magnitude and to choose shifted or unshifted paths for multiplication and division by 2.

TODO: Label the two data inputs, select signal, and output in this component view.

## Two-adder arithmetic stage in the calculator

![The two adders and surrounding colored signal paths inside the calculator](images/calculator-two-adders.png)

The blue wiring carries the second input, B, into the conditional inversion circuitry. In subtraction mode, B is inverted and a carry-in of 1 is supplied to the first adder, forming `A + ~B + 1`.

If the result is negative, the second adder converts it to a positive magnitude by inverting it and adding 1. The magnitude-selection multiplexer chooses the second result for negative subtraction answers and the first result otherwise. This stage comes before the multiply/divide multiplexers.

TODO: Add labels marking both adders, their carry connections, and the magnitude-selection multiplexer.

## Negative-result detector in the calculator

![Close view of the carry-out and subtraction-control wiring used by the negative detector](images/negative-detector.png)

The green path carries the first adder's carry-out. The yellow path carries the addition/subtraction control. The detector combines subtraction enabled with the inverse of carry-out:

`negative = subtract_enabled AND NOT first_adder_carry_out`

| Subtraction enabled | First carry-out | Negative signal |
| --- | --- | --- |
| No | Off | Off |
| No | On | Off |
| Yes | Off | On |
| Yes | On | Off |

During subtraction, a missing carry-out indicates a borrow: A is smaller than B. This enables the negative sign and selects the second adder's magnitude. Carry-out here is an unsigned carry/borrow indication, rather than signed overflow.

For `3 − 8`, carry-out is off, the negative signal is on, and the selected magnitude is 5.

## Double dabble converter: layout and built module

![Simplified layout of the double dabble converter](images/double-dabble-layout.png)

The simplified layout shows the repeated conversion stages. The purple bars represent the shift-and-conditional-add-3 structure.

![Fully built standalone double dabble converter](images/double-dabble-built.png)

The corresponding built converter is shown separately from the calculator. See [binary-to-BCD conversion](CALCULATOR.md#binary-to-bcd-conversion) for the algorithm description.

## Digit decoder and seven-segment wiring

![Standalone digit decoder viewed from the display side](images/display-decoder-front.png)

![Standalone digit decoder viewed from the input and wiring side](images/display-decoder-back.png)

These two views show the same standalone digit-display component. The purple circuitry decodes four BCD bits into one of ten selections, 0 through 9. The white wiring converts that selection into the required seven-segment pattern. The hundreds, tens, and ones positions each use their own decoder.

The thousands position uses a simplified driver to show 1 or remain blank. The lower three positions retain leading zeros. The minus sign and `.5` are separate fixed patterns enabled by their respective signals.

## Display circuitry in the assembled calculator

![Rear view of digit decoders and segment wiring installed behind the calculator display](images/display-installed-rear.png)

![Angled view of installed segment wiring and connections to the display](images/display-installed-angle.png)

These views show the digit-decoding and segment circuitry implemented behind the calculator's display. The double dabble converter supplies the whole-number digit values, while the sign and half-value signals control their fixed patterns separately.

## Assembled front panel

![Input levers labeled 128 through 1 from left to right](images/input-bit-labels.png)

Facing the panel, the left input bank is A and the right is B. Each bank accepts 0–255, with bit weights descending from 128 on the left to 1 on the right. Negative inputs are not supported.

![Labeled addition/subtraction, multiply, and divide controls](images/operation-labels.png)

The central controls run left to right: ADD / SUB (off for addition, on for subtraction), ANS × 2, and ANS / 2. Subtraction calculates A minus B.

![Calculator front panel with binary inputs and output below the decimal display](images/calculator-front.png)

The front panel brings the inputs, operation controls, binary output, sign indication, and seven-segment display together. The final result has 10 whole-number magnitude bits, a separate negative-sign bit, and a fractional bit worth 0.5.

The fractional bit directly enables a fixed `.5` display. When the bit is off, the fractional display is blank.

TODO: Add paired screenshots showing input settings and settled outputs for addition, negative subtraction, odd-result division, and both shift controls enabled.

## Display design credit

The builder credits Mattbatwings' [display-design tutorial at 20:25](https://www.youtube.com/watch?v=mDLfUbAK9T0&t=1225s) as the reference for the binary-to-decimal display design.
