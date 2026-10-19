# Adding Component Documentation

[Project overview](../README.md) · [Working calculator](../calculator/README.md)

This section is for documenting individual logic gates and reusable circuits separately from the calculator. A component can have its own screenshots, input/output explanation, truth table, design credits, and a link to where it is used in a larger build.

The standalone examples below are separate from the assembled calculator. See the [calculator component gallery](../calculator/COMPONENTS.md) for the circuits installed in it. Standalone AND and XOR gate pages can be added here when their screenshots and descriptions are ready.

## Four-bit ripple-carry adder

![Standalone four-bit ripple-carry adder](images/four-bit-adder.png)

This separate four-bit example illustrates the ripple-carry design. Carry propagates from each bit to the next more significant bit. The calculator uses two adders in its arithmetic stage; see the [implemented arithmetic circuitry](../calculator/COMPONENTS.md#two-adder-arithmetic-stage-in-the-calculator).

## Multiplexer

![Standalone multiplexer with separate input and control wiring](images/multiplexer.png)

A multiplexer selects between two input paths. The calculator uses multiplexers for magnitude selection and shift control. This screenshot shows the standalone example, rather than one installed in the calculator.

TODO: Label the data inputs, control signal, and output.

## Double dabble converter

![Simplified standalone double dabble layout](images/double-dabble-layout.png)

The layout model shows the repeated shift-and-conditional-add-3 stages, marked by purple bars.

![Fully built standalone double dabble converter](images/double-dabble-built.png)

This built module is separate from the calculator and is not connected to it in this view. See the [calculator conversion description](../calculator/README.md#binary-to-bcd-conversion) for its role in the output path.

## Digit decoder and seven-segment wiring

![Standalone digit decoder viewed from the display side](images/display-decoder-front.png)

![Standalone digit decoder viewed from the input and wiring side](images/display-decoder-back.png)

These are two views of a separate demonstration component. Purple circuitry decodes four BCD bits into one of ten digit selections, 0 through 9; white wiring maps that selection to the display segments. See the [installed display circuitry](../calculator/COMPONENTS.md#display-circuitry-in-the-assembled-calculator) for its implementation in the calculator.

The builder credits Mattbatwings' [display-design tutorial at 20:25](https://www.youtube.com/watch?v=mDLfUbAK9T0&t=1225s) as the display reference.

## Adding a component

Create a folder for each component, such as `and-gate/`, and put a `README.md` and an `images/` folder inside it. This keeps the description and its screenshots together. Add a link here after creating the page:

```markdown
- [AND gate](and-gate/README.md)
- [XOR gate](xor-gate/README.md)
```

Those are example links; the gate pages have not been added yet.

## Formatting screenshots

Inside a component's README, use a heading, image, and caption. Image paths are relative to the Markdown file containing them. For example, this refers to `components/and-gate/images/standalone.png` from `components/and-gate/README.md`:

```markdown
## Standalone circuit

![Standalone AND gate with inputs A and B and an output lamp](images/standalone.png)

Inputs A and B are controlled by the two levers. The lamp indicates the output.

## In the assembled build

![The same gate connected inside a larger circuit](images/implemented.png)

Describe the connected signals and what this gate does at this location.
```

The captions above are examples to adapt to the actual screenshots. Add the implementation section only when you have identified where that circuit is used.

For a smaller displayed image, use HTML in the README:

```html
<img src="images/standalone.png" alt="Standalone AND gate" width="700">
```

This changes its displayed size without changing the original image file.

## Reusable component page template

Copy the template below into the new component's README and replace the TODOs. Uncomment image lines after uploading the matching files.

```markdown
# Component name

[Component library](../README.md) · [Project overview](../../README.md)

TODO: Explain what the component does.

## Inputs and output

TODO: Name each input, the output, and any control signals.

## Standalone circuit

<!-- ![Describe the standalone circuit](images/standalone.png) -->

TODO: Explain the screenshot, including wire colors and signal direction.

## Behavior

TODO: Add a truth table for a gate, or example inputs and expected outputs
for a larger circuit. Mark which examples have been tested in the world.

## Use in a larger build

TODO: Identify a confirmed use and link to it, or state that this is currently
a standalone example.

<!-- ![Describe the component in use](images/implemented.png) -->

## Design credit

TODO: State whether this is an original design, an adaptation, or a tutorial
build. Link to the source where applicable.
```
