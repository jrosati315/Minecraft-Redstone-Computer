# Computer Design: Running Snake

[Project overview](../README.md) · [Working calculator](../calculator/README.md) · [Component library](../components/README.md)

My goal is to run Snake on a programmable Redstone computer with a graphical display and player controls. I'm following the general architecture taught in Mattbatwings' computer-building series, while working backward from Snake to choose the processor's operations, storage, and interfaces. The completed calculator was a practice project for arithmetic logic, binary conversion, and display circuitry. This page describes the planned computer.

## Proposed architecture

![Proposed Snake computer architecture](images/snake-computer-architecture.png)

[Editable SVG diagram](images/snake-computer-architecture.svg) · [Full-size PNG](images/snake-computer-architecture.png)

The diagram shows the intended functional outline, not a finished wiring schematic. It includes selected data and control paths; instruction bit positions, bus widths, clock phases, and all individual control signals are deliberately unspecified at this stage. Line crossings do not imply connections unless the paths share an endpoint or branch. The rectangular SELECT blocks represent multiplexers that route one of several values onto a shared path.

| Block | Intended role |
| --- | --- |
| Program counter and next-PC selector | Advance to the next instruction or select a branch, jump, or return address |
| Program memory | Supply the instructions that implement the game |
| Decode and control | Interpret instructions and enable the appropriate register, ALU, storage, and I/O actions |
| Register file | Hold working values and provide operands to the datapath |
| Immediate path and operand selector | Format a constant from an instruction and choose between it and a register value |
| ALU and flags | Calculate results and supply status for conditional decisions |
| Write-back selector | Choose an ALU result, loaded value, or input value to write into a register |
| Call stack | Hold return addresses if the program uses subroutine calls; optional for the initial design |
| Data storage | Hold game state beyond the working registers if required by the chosen representation |
| Input/output interface | Read player controls and send values or commands to the display |
| Graphical display | Show the Snake playfield |

The reference architecture includes data memory and a call stack. I have retained both in the outline so their roles are explicit, without committing to their final implementation or capacity. The call stack stores return addresses; it is different from the storage used for the snake's body. The CPU boundary identifies the processor circuitry, while program storage, additional data storage, and game input/output sit around it.

## Architecture reference

I use Mattbatwings' [Let's Make a Redstone Computer! series](https://www.youtube.com/playlist?list=PL5LiOvrbVo8nPTtdXAdSmDWzu85zzdgRT) as a learning reference for the architecture and the steps involved in building each part. This diagram is redrawn with a different layout, color scheme, and selector symbols, with game input/output added for the Snake goal. The underlying architecture is credited to that reference; the Snake-specific requirements and final implementation are the focus of my build.

## Target behavior

The game will advance a snake across a grid, accept direction changes, place food, grow the snake when it eats, and detect collisions. The display will show the snake and food. A game-over state and restart behavior are part of the target.

The playfield dimensions, maximum snake length, wall behavior, and target movement speed are not fixed yet. These choices determine the size and performance needed from the hardware. Food placement needs a way to choose an unoccupied cell; a simple pseudo-random generator or a deterministic candidate sequence can provide candidates without requiring a hardware random-number source.

## What counts as the CPU

The CPU is the circuitry that executes instructions. In this design, that means the ALU, working registers, instruction decoder and control circuitry, and the program counter that identifies the next instruction. An instruction register may hold the current instruction, depending on the sequencing design. Connections and multiplexers move values among these parts.

Program storage supplies the instructions. The display, its controller, player inputs, and any additional data storage complete the computer around the CPU. Program storage can be separate from writable game-state storage; its physical implementation is a design choice.

The register file is a bank of working registers selected for reads and writes. It is normally part of the CPU. A separate main RAM module is not a requirement for a small programmable computer if its registers and other state storage provide enough capacity and access for the program.

Registers are memory in the broad sense. The distinction here is their role and how instructions access them, rather than whether Redstone registers count as storage. Storage accessed as a general addressable data array can serve as main memory, even when it is physically built from registers.

## Working backward from the game

| Game behavior | Required capability | Possible implementation |
| --- | --- | --- |
| Move the head | Update a coordinate by one cell | Add or subtract a direction offset |
| Read controls | Capture a direction request between game updates | Input latch or input register |
| Detect food or collisions | Compare positions or inspect occupied cells | Equality checks and conditional branches |
| Move and grow the body | Remember the body's positions or movement history | Register bank, circular buffer, or another storage layout |
| Draw a game update | Light the new head cell and clear the departing tail cell when appropriate | Display commands or writes to stored pixel state |
| Place food | Choose and check an unoccupied location | Candidate generator plus occupancy check |
| Repeat and restart | Execute loops and change control flow | Program counter, branches, and initialization instructions |

These are capabilities, not a finalized instruction list. Reading input, writing the display, moving data, and branching are processor or system functions; they do not all belong inside the ALU.

## ALU direction

Addition, subtraction, and zero or equality detection are useful starting points. Depending on the state representation, bitwise logic, shifts, carry or borrow signals, or unsigned comparisons may also help. Comparisons can be provided by a subtraction result or separate comparison circuitry; each comparison does not require a separate arithmetic unit.

General multiplication, general division, fractional arithmetic, and binary-to-decimal conversion are not inherently needed for the core game. Coordinates can be maintained directly, and movement uses small offsets. Score display and other optional features may introduce additional needs.

The final ALU operations will follow a sketch of the game program and the chosen data representation. The existing calculator's ten magnitude bits, separate sign, and half-value output do not dictate the CPU's internal number format.

## Storage budget

The head and food positions alone are insufficient to represent a growing snake. The program also needs a representation of the body, direction, length, and any indices used to update that body. Collision detection may use a scan of body positions or a separate occupancy map. The display may hold its own pixel state or be refreshed from other storage.

As an example, a 16 by 16 playfield has 256 cells. One position can be packed into eight bits: four for X and four for Y. A representation storing one byte per body position would use 64 bytes for a maximum length of 64 cells, before other game variables and scratch space. This is an illustration, not a chosen size or a minimum storage requirement; direction histories and other encodings have different costs.

If the CPU selects registers only through fixed register numbers in instructions, updating a variable-length body can require extra code or selection circuitry. Indirect access, a dedicated body buffer, or a shift-register representation are alternatives. The register-file size and access method therefore need to be considered together.

## Display and timing

The graphical playfield is a new subsystem. The calculator's decimal decoder can remain useful for a score or debugging display, but drawing Snake needs a way to select cells and change their displayed state.

CPU execution and game movement have different timing needs. The processor can execute many instructions between movement steps. Input should be retained long enough for the program to read it, and the game should update its position at a controlled interval. The required clock rate depends on Redstone propagation delays, the number of instructions per update, and the intended play speed.

## Design direction

The next design work is to choose the grid and maximum length, sketch the game-state layout and update loop, and define how the program accesses instructions, registers, input, and the display. Those decisions will determine the instruction set and ALU before the complete processor is built.

The intended result is a programmable computer that runs Snake as its target application. A circuit with permanently wired Snake behavior would instead be a dedicated game controller. Instruction execution, rather than the presence of a separate RAM module, distinguishes the planned CPU from the existing manual calculator.
