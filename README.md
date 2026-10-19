# Minecraft Redstone Computer

I'm building a computer in Minecraft using Redstone. The current milestone is a working 8-bit calculator, with a decimal display and binary output. This repository documents the calculator and the standalone logic circuits I've built along the way.

[Watch the demonstration](https://youtu.be/XQKjd9Awp-k) · [Download the world](https://github.com/rosatij1/Minecraft-Redstone-Computer/releases/tag/v0.1.0)

## Current build

The calculator accepts two unsigned 8-bit inputs, each from 0 to 255, entered using levers. It supports:

- Addition and subtraction, including negative answers
- Multiplication and division by 2 using bit shifts
- Half-value results, displayed as `.5`
- Binary output and a decimal seven-segment display

Its 12 output bits consist of 10 whole-number magnitude bits, one negative-sign bit, and one half-value bit. Subtraction uses two's complement internally, then converts negative answers to a separate sign and magnitude for display.

The circuit is combinational: changing the inputs or operation switches updates the answer after the signals settle. There is no clock or calculate button. Multiplication is applied before division; enabling both shift controls preserves the original arithmetic result.

![Calculator front panel](calculator/images/calculator-front.png)

The left input bank is A and the right is B. Subtraction calculates `A − B`. See the [calculator documentation](calculator/README.md) for controls, output representation, and circuit design.

## Download and run

**Minecraft Java Edition 1.18.2 — tested in vanilla, with no mods required.**

1. Download [redstone-computer-v0.1.0-mc1.18.2.zip](https://github.com/rosatij1/Minecraft-Redstone-Computer/releases/download/v0.1.0/redstone-computer-v0.1.0-mc1.18.2.zip).
2. Extract the ZIP and find the world folder containing `level.dat`.
3. With Minecraft closed, copy that entire folder into your installation's `saves` folder. On a default Windows installation, press Windows+R and enter `%appdata%\.minecraft\saves`.
4. Launch Java Edition 1.18.2 and open the world from Singleplayer.
5. Set the calculator's input levers and operation switches, then allow the output to settle.

I used WorldEdit to place vanilla blocks and Carpet to accelerate ticks and move through walls during construction and testing. Neither mod is required to run the world.

## Explore the project

- [Calculator](calculator/README.md) — controls and arithmetic, conversion, and display stages
- [Calculator gallery](calculator/COMPONENTS.md) — circuits installed in the assembled build
- [Standalone component library](components/README.md) — gates, adders, multiplexers, and display circuits
- [Demonstration](calculator/videos/README.md) — video and example results

## Next stage

The calculator is a foundation for the larger computer. My next stage is to develop the CPU architecture, memory, instruction set, and control logic, then connect the subsystems. The full computer is in development.
