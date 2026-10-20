# Standalone Redstone Components

[Project overview](../README.md) · [Working calculator](../calculator/README.md)

These standalone gates and circuits are separate from the assembled calculator. See the [calculator gallery](../calculator/COMPONENTS.md) for the components installed in it.

The next system goal is a [programmable computer that runs Snake](../design/README.md), using an architecture inspired by Mattbatwings' computer-building series. The calculator was my initial completed practice project for arithmetic logic, binary conversion, and displays. The gates, adders, and multiplexers provide building blocks for the future datapath and control circuitry. The double-dabble converter and seven-segment circuitry belong to the existing decimal display; they are not prerequisites for the graphical Snake playfield.

| Component | Contents |
| --- | --- |
| [NOT gate](not-gate/README.md) | Single-input inverter, screenshot, and truth table |
| [AND gate](and-gate/README.md) | Screenshot and truth table |
| [OR gate](or-gate/README.md) | Screenshot and truth table |
| [NAND gate](nand-gate/README.md) | Screenshot and truth table |
| [NOR gate](nor-gate/README.md) | Screenshot and logic; identification based on visible wiring |
| [XOR gate](xor-gate/README.md) | Screenshot and truth table |
| [Half adder](half-adder/README.md) | Two inputs, sum, and carry |
| [Full adder](full-adder/README.md) | Two inputs plus carry-in; sum and carry-out |
| [Ripple-carry adders](ripple-carry-adder/README.md) | Eight-bit and four-bit examples, logic, and calculator application |
| [Multiplexer](multiplexer/README.md) | Selection logic and standalone screenshot |
| [Double dabble converter](double-dabble/README.md) | Layout model, built module, and algorithm |
| [Digit decoder and display](seven-segment-display/README.md) | Two standalone views and design credit |

See the [standalone circuit gallery](AUTHORING.md) for larger circuit examples and layout views.

Truth tables describe the expected logical behavior of each component.
