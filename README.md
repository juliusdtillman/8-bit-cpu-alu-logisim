# 8 Bit CPU and ALU in Logisim

I built this circuit in Logisim to get a better understanding of how a processor works. It has two 8 bit registers that hold numbers and an ALU that can do math and logic operations. A 4 bit opcode lets me choose what the circuit does. I can also reset the registers, check the result flags, and save a result back into Register A.

This is a small CPU datapath, not a complete CPU that can run programs. It does not have instruction memory or a program counter.

![The registers and ALU operations](docs/images/registers-and-alu.png)

## What it does

* Stores two 8 bit values in Registers A and B
* Runs 14 math and logic operations
* Uses a 4 bit opcode to choose an operation
* Shows the answer on an 8 bit output
* Shows zero, carry, and comparison flags
* Lets me save an ALU result back into Register A
* Uses a clock and reset to control the registers

## How to try it

1. Open [the circuit file](circuit/8-bit-cpu-alu.circ) in Logisim 2.7.1.
2. Make sure **Simulation Enabled** is checked under **Simulate**.
3. Use the Poke Tool to set `DATA_A` to `00000011` and `DATA_B` to `00000010`.
4. Set `LOAD_A` and `LOAD_B` to `1`. Keep `RESET` and `WRITEBACK_A` at `0`.
5. Set `CLOCK` to `0`, then click it to change it to `1`.
6. Set `OPCODE_4bit` to `0000` for addition.

Register A should show 3, Register B should show 2, and the output should show 5, or `00000101` in binary.

To try another operation, change the opcode. You do not have to reload the registers unless you want different input numbers.

## Operations

| Opcode | Name | What it does |
| :---: | :--- | :--- |
| `0000` | ADD | A plus B |
| `0001` | INC | A plus 1 |
| `0010` | DEC | A minus 1 |
| `0011` | CMP | Compares A and B |
| `0100` | NOT | Flips the bits in A |
| `0101` | AND | Bitwise AND |
| `0110` | OR | Bitwise OR |
| `0111` | SHR | Shifts A right by 1 |
| `1000` | SHL | Shifts A left by 1 |
| `1001` | SUB | A minus B |
| `1010` | XOR | Bitwise XOR |
| `1011` | NAND | Bitwise NAND |
| `1100` | NOR | Bitwise NOR |
| `1101` | XNOR | Bitwise XNOR |
| `1110` | Reserved | No operation added |
| `1111` | Reserved | No operation added |

For CMP, the result output shows A while the comparison flags show whether A is equal to, less than, or greater than B.

## Testing

I tested the circuit in Logisim with 21 checks. They covered all 14 operations, register loading and holding, reset, saving a result back into Register A, and the main status flags. Those checks passed on the version before I cleaned up the long MUX wires.

I then changed the MUX wiring layout to make the connections shorter and straighter. A comparison of the circuit files confirmed that the operations, component settings, and numbered MUX connections stayed the same. I have not repeated the full 21 tests on this latest layout.

You can read the [test notes](docs/TESTING.md) and [circuit explanation](docs/ARCHITECTURE.md).

## Screenshots

![The output MUX and status flags](docs/images/mux-and-status-flags.png)

## Files

* [Circuit to open in Logisim](circuit/8-bit-cpu-alu.circ)
* [Circuit explanation](docs/ARCHITECTURE.md)
* [Test results](docs/TESTING.md)
* [More screenshots](docs/images)
