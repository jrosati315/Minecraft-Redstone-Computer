# Computer Design: Running Snake

[Project overview](../README.md) · [Working calculator](../calculator/README.md) · [Component library](../components/README.md)

I want this computer to run Snake on a graphical display with player controls. I'm following Mattbatwings' computer-building series and using the game to decide which operations, storage, and interfaces to build. The calculator was practice for the arithmetic and display circuits. The computer described here is still being designed.

## Proposed architecture

![Proposed Snake computer architecture](images/snake-computer-architecture.png)

[Editable SVG diagram](images/snake-computer-architecture.svg) · [Full-size PNG](images/snake-computer-architecture.png)

The diagram shows how the main parts will connect. It includes selected data and control paths; I haven't set the instruction bit positions, bus widths, clock phases, or every control signal yet. Crossing lines connect only where they share an endpoint or branch. Each rectangular SELECT block is a multiplexer that chooses which value to pass along.

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

Mattbatwings' architecture includes data memory and a call stack, so I've kept both in the outline while I work out their size and role. A call stack holds return addresses, separate from the snake's body data. The CPU boundary encloses the processor. Program memory, additional data storage, and the game's input and output sit outside it.

## Architecture reference

I'm learning the architecture and how to build each part from Mattbatwings' [Let's Make a Redstone Computer! series](https://www.youtube.com/playlist?list=PL5LiOvrbVo8nPTtdXAdSmDWzu85zzdgRT). The diagram redraws that architecture and adds the game's input and display. I'll adapt the hardware and instructions to run Snake.

## Target behavior

The player will steer a snake around a grid and collect food to grow. The computer will move the body, check for collisions, and draw the snake and food. The game will also need a game-over state and a way to restart.

I haven't chosen the grid size, maximum snake length, wall behavior, or movement speed yet. Those choices affect storage capacity and how quickly the computer must run. Food must appear in an empty cell. A simple pseudo-random generator or a fixed sequence of candidate cells could handle that, with an occupancy check before placing food.

## What counts as the CPU

The CPU executes instructions. It contains the ALU, working registers, instruction decoder, control circuitry, and program counter. Depending on the timing design, an instruction register may hold the current instruction. Wires and multiplexers move values between these parts.

Program storage supplies the instructions. The display controller, screen, player inputs, and any additional data storage connect to the CPU. Instructions can be stored separately from writable game data.

The register file holds the working values the CPU reads and writes. A small computer can run without separate main RAM if the registers and other storage hold everything its program needs and let it access those values.

Registers store data, too. Their role and access method distinguish them from main memory. A general addressable array can serve as main memory even if it is built from individual Redstone registers.

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

This table describes what the computer must do. The instruction list comes later. Input, display writes, data transfers, and branches need support from the processor and surrounding circuits as well as the ALU.

## ALU direction

I'll start with addition, subtraction, and zero or equality detection. Bitwise logic, shifts, carry or borrow signals, and unsigned comparisons may help once I've chosen how to store the game state. A comparison can use subtraction or separate comparison circuitry; it doesn't need its own arithmetic unit for every condition.

Core Snake can use whole-number coordinates and small movement offsets, without general multiplication, division, fractional arithmetic, or decimal conversion. A score display or other additions may need more operations.

Before fixing the ALU operations, I'll sketch the game program and its data layout. The calculator's ten magnitude bits, separate sign, and half-value output don't set the CPU's number format.

## Storage budget

The program has to remember the body as well as the head and food positions. It also needs the direction, length, and any indices used to update the body. Collision detection could scan stored body positions or use an occupancy map. The screen could hold its own pixel state or be refreshed from other storage.

For example, a 16×16 grid has 256 cells. One position fits in eight bits: four for X and four for Y. Storing one byte per body position would take 64 bytes for a 64-cell snake, plus space for other variables and temporary values. I haven't chosen that grid or storage method. A direction history or another encoding would use a different amount of space.

If instructions can only select fixed register numbers, updating a growing body may take extra code or selection circuits. Indirect access, a dedicated body buffer, or shift registers offer other options. I'll choose the register-file size and access method together.

## Display and timing

The game needs a new graphical display with a way to select cells and turn them on or off. The calculator's decimal decoder could still serve a score or debugging display.

The processor can execute many instructions between game moves. Input must stay available long enough for the program to read it, and movement needs a controlled interval. Redstone propagation delays, instructions per update, and the intended play speed will determine the clock rate.

## Design direction

Next I'll choose the grid and maximum snake length, sketch the update loop and storage layout, and decide how the program accesses registers, instructions, controls, and the screen. That gives me a basis for choosing the instruction set and ALU before building the processor.

The goal is to load a program that runs Snake. The CPU will execute that program, rather than having the game behavior permanently wired into it.
