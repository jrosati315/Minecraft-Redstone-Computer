# 8-Bit Calculator Practice Build

[Back to the main project README](../README.md) · [Standalone component library](../components/README.md)

[Watch the calculator demonstration](https://youtu.be/XQKjd9Awp-k) · [Video and example results](videos/README.md)

I built this calculator to practice arithmetic logic, binary-to-BCD conversion, and display circuitry before starting the computer. It gave me a complete project to finish first. Two banks of levers accept unsigned 8-bit numbers from 0 to 255, and the answer appears on binary indicators and a seven-segment display.

## Confirmed working features

| Feature | Current behavior |
| --- | --- |
| Addition | Adds two 8-bit numbers |
| Subtraction | Subtracts two 8-bit numbers using two's complement in the ALU |
| Multiply by 2 | Shifts the arithmetic result left |
| Divide by 2 | Shifts the arithmetic result right and displays `.5` for an odd result |
| Both shift controls enabled | The shifts cancel, leaving the arithmetic result unchanged |
| Result handling | 12 output signals: 10 whole-number magnitude bits, one sign bit, and one half-value bit |
| Binary-to-BCD conversion | Converts 10 magnitude bits into four decimal digit positions using double dabble |
| Display output | Separate digit decoders and segment wiring; thousands position shows 1 or stays blank |
| Automatic updates | Uses combinational logic; no clock or calculate button is needed |

## Front panel and operation

![Calculator input levers, central operation switches, and binary output indicators](images/calculator-controls.png)

Facing the front panel, the left bank of eight levers is input A and the right bank is input B. Both inputs are unsigned values from 0 to 255; negative numbers cannot be entered directly. Subtraction calculates `A − B`, so the output can still be negative.

Within each bank, the bit weights run from left to right as `128, 64, 32, 16, 8, 4, 2, 1`. Turn on the levers whose weights sum to the desired value. For example, 13 uses the 8, 4, and 1 levers, giving binary `00001101`.

![Input bank with each lever labeled by its binary weight](images/input-bit-labels.png)

Three control switches sit between the input banks. From left to right:

| Sign label | Off | On |
| --- | --- | --- |
| ADD / SUB | Addition: `A + B` | Subtraction: `A − B` |
| ANS × 2 | No multiplication | Multiply the arithmetic result by 2 |
| ANS / 2 | No division | Divide the result after the multiply stage by 2 |

Here, on means the lever's powered state. With both shift controls on, multiplication and division cancel.

![Close-up of the three labeled operation switches](images/operation-labels.png)

Above the controls, the binary output includes a negative indicator. The large seven-segment display sits at the top of the panel.

The calculator uses **combinational logic**: changing an input or operation switch changes the output after the Redstone signals settle. It has no clock or calculate button.

To use the calculator, enter A and B in binary with their lever banks, select addition or subtraction, and set the shift controls as needed. Allow the output to settle before reading the result.

## How the calculator is organized

The inputs pass through two adders, a multiplexer that selects the magnitude, and the multiply/divide stages. The result then goes to the converter and display. A separate signal controls the negative sign.

### Arithmetic logic unit

The arithmetic stage uses two ripple-carry adders. Each bit passes its carry to the next more significant bit. The first adder handles addition or subtraction; the second converts a negative subtraction result to a positive magnitude for the display path.

In addition mode, the first adder calculates `A + B`, and its result is selected. Addition can require a ninth result bit.

In subtraction mode, B's bits are inverted and the first adder receives a carry-in of 1, giving `A + ~B + 1`. The negative detector combines the subtraction control with the inverted carry-out:

`negative = subtract_enabled AND NOT first_adder_carry_out`

During subtraction, no carry-out means A is smaller than B. The negative detector then selects the second adder, which inverts the first result and adds 1 to get its magnitude. Otherwise, the multiplexer selects the first adder. The sign travels separately from the magnitude.

For example, with `3 − 8`, the first adder has no carry-out, so the negative detector turns on. The second adder produces a magnitude of 5, and the separate sign signal indicates a negative answer. The magnitude then enters the multiply/divide shift stages.

![The two adders and surrounding wiring in the assembled calculator](images/calculator-two-adders.png)

See the [calculator component gallery](COMPONENTS.md) for circuitry installed in the calculator, and the [standalone component library](../components/README.md) for the separate four-bit adder and multiplexer examples.

### Bit-shift operations

The shift controls act on the result of addition or subtraction, before output conversion and display. Multiplexers select between the shifted and unshifted signal paths.

The multiply-by-2 stage comes first. When enabled, it moves the result's bits one position to the left. Its output feeds the divide-by-2 stage, which moves the bits one position to the right when enabled. With both controls enabled, the shifts cancel and the original arithmetic result is preserved.

| Multiply by 2 | Divide by 2 | Output |
| --- | --- | --- |
| Off | Off | Original arithmetic result |
| On | Off | Arithmetic result multiplied by 2 |
| Off | On | Arithmetic result divided by 2 |
| On | On | Original arithmetic result |

The 10-bit magnitude leaves room to multiply the answer by 2. When dividing by 2, the lowest whole-number bit shifts into a separate position worth one half. That keeps the remainder of an odd result: binary `0.1` equals decimal `0.5`. The fractional bit turns a fixed `.5` display on or off. This is a right shift because the bits move to lower place values, regardless of how the wiring is arranged in Minecraft.

### Output representation

The output has 12 bits:

| Field | Signals | Meaning |
| --- | --- | --- |
| Negative sign | 1 | Indicates a negative answer |
| Whole-number magnitude | 10 | Unsigned whole-number part of the answer |
| Fraction | 1 | Adds `0.5` to the magnitude when set |

The final answer uses sign-and-magnitude representation with one fractional bit. The sign applies to both the whole-number magnitude and the fraction. Subtraction uses two's complement inside the arithmetic stage, but the 12 output bits are not a single two's-complement integer.

For example, dividing a magnitude of 5 by 2 produces a whole-number magnitude of 2 and a half-value bit of 1, representing 2.5. The demonstration shows a negative fractional output of -002.5 at approximately 0:41; see the [video examples](videos/README.md).

### Binary-to-BCD conversion

The calculator uses **double dabble**, also called shift-and-add-3, to convert the 10 magnitude bits into thousands, hundreds, tens, and ones. Each BCD digit uses four bits to encode 0 through 9. The thousands position only needs 0 or 1 for a 10-bit magnitude.

During the conversion, the binary value is shifted through a sequence of stages. Before each shift, any BCD digit that is 5 or greater has 3 added to it. Repeating that process produces the decimal digits in BCD form. The separate sign and half-value signals bypass this conversion.

The separate layout model and standalone converter are documented on the [converter page](../components/double-dabble/README.md).

### Seven-segment output

Each of the hundreds, tens, and ones digits has its own decoding circuitry. The purple circuit decodes the digit's four BCD input bits into one of ten digit-selection signals, representing 0 through 9. The white wiring maps the selected digit to the segments that must light up.

![Digit-decoding and segment circuitry installed behind the calculator display](images/display-installed-rear.png)

The thousands position uses a simple driver that shows 1 or stays blank. This allows results above 999, up to `(255 + 255) × 2 = 1020`. The [demonstration](videos/README.md) shows 510 from addition, then 1020 after multiplication at about 1:06.

The hundreds, tens, and ones positions keep their leading zeros. Five appears as `005`, with the thousands position blank.

The negative signal lights a fixed minus sign. The panel also shows the binary result and a negative indicator below the main display.

The half-value bit directly lights a fixed `.5` pattern. When the bit is off, that part of the display stays blank. It bypasses the BCD converter and digit decoders.

![Full calculator front panel with the seven-segment display above the binary output and controls](images/calculator-front.png)

See the [installed display gallery](COMPONENTS.md#display-circuitry-in-the-assembled-calculator) for another view of the implemented circuitry. The separate demonstration decoder is on the [display component page](../components/seven-segment-display/README.md).

## Design references and credits

I used Mattbatwings' YouTube videos to learn the circuits, including some of the decoder designs. [This display-design tutorial at 20:25](https://www.youtube.com/watch?v=mDLfUbAK9T0&t=1225s) was my reference for the binary-to-decimal display design.

## Relationship to the full computer

The calculator gave me practice with the parts I'll need for the [Snake computer](../design/README.md), especially arithmetic, carry handling, multiplexers, binary conversion, and display decoding. I may reuse individual circuit designs, but I don't plan to treat the assembled calculator as the finished CPU.

The 12-bit output format belongs to this calculator. The CPU's word size, instruction width, and operations will depend on what Snake needs.

Snake will need a graphical screen, player input, and storage for the game state. It will also need a processor that sequences instructions and updates stored values, beyond the combinational circuitry used here.
