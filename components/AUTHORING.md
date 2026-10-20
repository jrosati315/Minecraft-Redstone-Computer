# Standalone Circuit Gallery

[Project overview](../README.md) · [Working calculator](../calculator/README.md)

These are standalone circuits I built alongside the calculator. The [calculator gallery](../calculator/COMPONENTS.md) shows the installed versions, and the [component library](README.md) lists the individual gates and circuits.

## Four-bit ripple-carry adder

![Standalone four-bit ripple-carry adder](images/four-bit-adder.png)

In this four-bit adder, each bit passes its carry to the next more significant bit. The calculator uses two adders in its arithmetic stage; see the [implemented arithmetic circuitry](../calculator/COMPONENTS.md#two-adder-arithmetic-stage-in-the-calculator).

## Multiplexer

![Standalone multiplexer with separate input and control wiring](images/multiplexer.png)

A multiplexer selects between two input paths. The calculator uses multiplexers for magnitude selection and shift control. This screenshot shows the standalone example, rather than one installed in the calculator.

## Double dabble converter

![Simplified standalone double dabble layout](images/double-dabble-layout.png)

The layout model shows the repeated shift-and-conditional-add-3 stages, marked by purple bars.

![Fully built standalone double dabble converter](images/double-dabble-built.png)

This is a separate converter module, shown without a connection to the calculator. See the [calculator conversion description](../calculator/README.md#binary-to-bcd-conversion) for its role in the output path.

## Digit decoder and seven-segment wiring

![Standalone digit decoder viewed from the display side](images/display-decoder-front.png)

![Standalone digit decoder viewed from the input and wiring side](images/display-decoder-back.png)

These two views show a standalone decoder. The purple circuitry decodes four BCD bits into a digit selection from 0 to 9. White wiring connects that selection to the display segments. See the [installed display circuitry](../calculator/COMPONENTS.md#display-circuitry-in-the-assembled-calculator) for its implementation in the calculator.

I used Mattbatwings' [display-design tutorial at 20:25](https://www.youtube.com/watch?v=mDLfUbAK9T0&t=1225s) as a reference for the display.
