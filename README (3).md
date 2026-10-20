# Double Dabble Binary-to-BCD Converter

[Component library](../README.md) · [Calculator](../../calculator/README.md)

Double dabble converts a binary value into decimal digits encoded in BCD. Each standard BCD digit uses four bits.

## Layout model

![Simplified standalone double dabble layout](../images/double-dabble-layout.png)

Purple bars mark the repeated shift-and-conditional-add-3 stages.

## Built module

![Standalone double dabble converter](../images/double-dabble-built.png)

This standalone converter is shown without a connection to the calculator.

## Algorithm

Starting with zeroed BCD digits, process the binary input from most significant bit to least significant bit. Before each shift, add 3 to every BCD digit whose value is at least 5. Shift the next input bit into the conversion path. After all bits have been processed, the BCD digits encode the decimal value.

The Redstone stages are combinational, so the signals pass through them without a clock stepping the conversion.

## Calculator implementation

Ten whole-number magnitude bits feed the converter, producing thousands, hundreds, tens, and ones. The thousands position can only be 0 or 1 for a ten-bit magnitude. Sign and half-value signals bypass this conversion. See the [calculator description](../../calculator/README.md#binary-to-bcd-conversion).
