# Minecraft Redstone Computer

This repository documents an ongoing computer build made in Minecraft with Redstone. The project is still in development. Its most complete subsystem is a working 8-bit calculator, which serves as a step toward the larger computer.

## Current progress

The calculator accepts two unsigned 8-bit values (0–255), entered manually in binary using levers. It uses combinational logic: the output updates automatically after signals propagate through the Redstone circuitry, with no clock or calculate button.

The calculator can:

- Add two 8-bit numbers
- Subtract two 8-bit numbers using two's complement, with a second adder producing the magnitude of negative results
- Multiply the arithmetic result by 2 with a left bit shift
- Divide the arithmetic result by 2 with a right bit shift, displaying `.5` for odd results
- Produce a 12-signal output: 10 whole-number magnitude bits, one negative-sign bit, and one half-value bit
- Convert binary output to BCD with the double dabble algorithm
- Drive a decimal seven-segment display through individual digit decoders, with a simplified thousands indicator and fixed minus-sign and `.5` patterns

Three control switches select addition or subtraction, enable multiplication by 2, and enable division by 2. The front panel includes binary output with a negative indicator and a large seven-segment display above it.

The shift controls act on the addition or subtraction result. Enabling both cancels the shifts and leaves that result unchanged.

Facing the panel, input A is on the left and B is on the right. Subtraction calculates `A − B`. Both inputs are nonnegative; negative answers are produced by subtraction.

See the [calculator README](calculator/README.md) for its operation and circuit design, and the [component library](components/README.md) for standalone gates and circuits.

## Project status

The calculator features above are working. The full computer and CPU are planned work, so their design and specifications are not documented as finished features yet.

### Planned development

- Build the calculator into a larger computer architecture
- Develop and document the CPU
- Record how the major subsystems connect
- Add diagrams, screenshots, and demonstration videos
- Document controls, inputs, outputs, and operating steps

## Gallery

![Front of the working calculator, showing its display, binary output, and input levers](calculator/images/calculator-front.png)

The working calculator's front panel. The two binary inputs sit along the bottom, with three operation switches between them. The binary result and negative indicator sit above the controls, below the large display.

A silent demonstration has been recorded. See the [video folder](calculator/videos/README.md) for upload status; the recording is not yet included in this bundle.

## Repository contents

- [`calculator/README.md`](calculator/README.md) — working calculator subsystem
- [`calculator/COMPONENTS.md`](calculator/COMPONENTS.md) — components installed in the assembled calculator
- [`components/README.md`](components/README.md) — library for standalone gates and reusable circuits
- Minecraft world download — the project world, if included in this repository
- `calculator/images/` — calculator screenshots
- [`calculator/videos/`](calculator/videos/README.md) — demonstration video location and upload status

## Running the world

The build uses Minecraft **1.18.2**. WorldEdit is used as a building tool and is the only mod reported as used during construction. Whether it is needed to run the finished world has not yet been confirmed.

### TODO

- [ ] Confirm the Minecraft edition
- [ ] Confirm whether the world runs without WorldEdit and document any required resource packs or settings
- [ ] Add the world-download filename and installation instructions
- [ ] Explain where the computer is located after the world loads
- [ ] Add recorded example calculations

## About this repository

This repository is both a record of the build process and a portfolio project. It will be updated as more of the computer is designed, built, tested, and documented.

