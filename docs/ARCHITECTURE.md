# How the circuit works

This project is a small 8 bit CPU datapath built in Logisim 2.7.1. It stores two numbers and uses an ALU to do math and logic operations. It does not run stored programs.

## Registers

Register A and Register B each hold one 8 bit number.

When `LOAD_A` or `LOAD_B` is set to `1`, the related register takes its input on the next rising clock edge. When the load value is `0`, it keeps its current number. Setting `RESET` to `1` clears both registers.

## ALU

The ALU reads the numbers from A and B. The circuit has 14 operation outputs named `OP00` through `OP13`.

A multiplexer uses `OPCODE_4bit` to choose which operation appears on `RESULT_8bit`. The last two opcode choices are reserved and do not run an operation.

## Write back

`WRITEBACK_A` controls the input to Register A. When it is `0`, the register can load the number from `DATA_A`. When it is `1`, it can load the selected ALU result instead. `LOAD_A` must still be set to `1`, and the clock must rise before A takes the new value.

For example, if A is 4 and B is 5, addition gives 9. Saving that answer into A makes the next addition 9 plus 5, which gives 14.

## Flags

| Flag | Meaning |
| :--- | :--- |
| `CMP_EQ` | A and B are equal |
| `CMP_LT` | A is less than B |
| `CMP_GT` | A is greater than B |
| `ADD_CARRY` | Addition went past the 8 bit limit |
| `ZERO` | The selected ALU answer is zero |
| `CU_ADD` | Addition opcode is selected |
| `CU_AND` | AND opcode is selected |
| `CU_SHR` | Right shift opcode is selected |

The comparison and carry flags come from their own circuits. They can still show values when another opcode is selected. The ZERO flag checks the currently selected ALU result.

## Things this project does not have

There is no program counter, instruction memory, or instruction execution cycle. This is a working ALU datapath with registers and controls, not a full programmable CPU.

The circuit has two reserved opcode values, `1110` and `1111`. They are not implemented instructions.

## Files

The editable circuit is in [the circuit folder](../circuit/8-bit-cpu-alu.circ). The [test record](TESTING.md) is also included. Screenshots of the final retest were captured separately.
