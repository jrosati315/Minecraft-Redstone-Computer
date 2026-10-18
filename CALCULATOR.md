# 8-Bit Calculator Subsystem

[Back to the main project README](README.md)

The calculator is the first working subsystem in the larger Minecraft Redstone computer project. It accepts two 8-bit numbers and performs arithmetic and bit-shift operations. Its output circuitry converts the result into a form that can be shown on seven-segment displays.

## Confirmed working features

| Feature | Current behavior |
| --- | --- |
| Addition | Adds two 8-bit numbers |
| Subtraction | Subtracts two 8-bit numbers using two's complement in the ALU |
| Result handling | Handles a 9-bit result, including negative results |
| Binary-to-BCD conversion | Converts binary output to BCD; the specific converter design still needs to be identified |
| Display output | Converts BCD/binary values for seven-segment output |
| Multiply by 2 | Shifts the bits left |
| Divide by 2 | Shifts the bits right |

## How the calculator is organized

The build currently includes an arithmetic logic unit (ALU), output-conversion circuitry, and seven-segment display circuitry. The exact circuit layout, component designs, and signal path still need to be documented.

### Arithmetic logic unit

The ALU performs addition and subtraction. Subtraction uses two's complement. Results may require a ninth bit, and the design can represent negative results.

> **Diagram placeholder:** Add an annotated screenshot of the ALU here.

<!-- After uploading the image, replace the placeholder above with:
![Annotated view of the calculator ALU](images/calculator-alu.png)
-->

### Binary-to-BCD conversion

The calculator uses a binary-to-BCD converter before sending values to the display system. The exact converter method or circuit has not yet been recorded.

> **Image placeholder:** Add a screenshot of the binary-to-BCD converter here.

<!-- After uploading the image, replace the placeholder above with:
![Binary-to-BCD converter](images/binary-to-bcd.png)
-->

### Seven-segment output

The output circuitry converts the result into the signals needed by the seven-segment display.

> **Image placeholder:** Add a clear screenshot of the display showing a result here.

<!-- After uploading the image, replace the placeholder above with:
![Calculator result on the seven-segment display](images/seven-segment-output.png)
-->

### Bit-shift operations

A left shift multiplies the value by 2, and a right shift divides it by 2. The behavior at the bit limits—including overflow, discarded bits, and signed values—still needs to be tested and documented.

## Suggested demonstrations

Add screenshots or short videos showing:

- A basic addition example
- A subtraction with a positive result
- A subtraction with a negative result
- A calculation that uses the ninth result bit
- Multiplication by 2 with a left shift
- Division by 2 with a right shift
- The input, conversion, and display stages in one continuous demonstration

## Documentation TODOs

- [ ] Identify the binary-to-BCD converter design or method
- [ ] Explain how two 8-bit inputs are entered
- [ ] Explain how the operation is selected
- [ ] Document how negative results are represented and displayed
- [ ] Clarify the exact 9-bit result behavior for addition and subtraction
- [ ] Test and document overflow and underflow behavior
- [ ] Test and document bit shifts for signed values and values at the 8-bit limit
- [ ] Record the seven-segment decoder design
- [ ] Add labeled screenshots of each major circuit
- [ ] Add example calculations with expected and observed outputs
- [ ] Add a video walkthrough

## Relationship to the full computer

This calculator is a working subsystem and a foundation for the planned computer. The full CPU architecture, instruction set, memory, control logic, and other computer specifications have not been confirmed and should be documented as they are designed and tested.
