# Testing notes

I checked the CPU and ALU in Logisim using a set of 21 manual tests on the final straight-wire MUX layout. All 21 tests passed. A shift direction problem found during testing of an earlier version was corrected before this final retest.

The 14 wires going into the result MUX were shortened and straightened without changing the operation mapping. After that layout change, I reran the full 21-test suite on the final circuit. Screenshots from the final checks show the SHR and XNOR results and the write-back result.

## ALU operations

For these checks, Register A had 3 and Register B had 2.

| Test | Opcode | Operation | Expected answer | Result |
| :---: | :---: | :--- | :--- | :--- |
| 1 | `0000` | ADD | 5 | Pass |
| 2 | `0101` | AND | 2 | Pass |
| 3 | `0110` | OR | 3 | Pass |
| 4 | `0111` | SHR | 1 | Pass |
| 5 | `1000` | SHL | 6 | Pass |
| 6 | `1001` | SUB | 1 | Pass |
| 7 | `1010` | XOR | 1 | Pass |
| 8 | `1011` | NAND | 253 | Pass |
| 9 | `1100` | NOR | 252 | Pass |
| 10 | `1101` | XNOR | 254 | Pass |
| 11 | `0001` | INC | 4 | Pass |
| 12 | `0010` | DEC | 2 | Pass |
| 13 | `0011` | CMP | A stays 3 on the result output and the greater flag is 1 | Pass |
| 14 | `0100` | NOT | 252 | Pass |

## Registers and flags

| Test | What was checked | Expected | Result |
| :---: | :--- | :--- | :--- |
| 15 | Register hold | A and B keep their values when loading is off | Pass |
| 16 | Reset | Both registers clear to 0 | Pass |
| 17 | Write back | A saves 9, B stays 5, and the next addition gives 14 | Pass |
| 18 | Zero flag | 5 minus 5 gives 0, so ZERO is 1 | Pass |
| 19 | Carry flag | 255 plus 1 wraps to 0 and shows a carry | Pass |
| 20 | Equal flag | 5 equals 5, so CMP_EQ is 1 | Pass |
| 21 | Less than flag | 2 is less than 5, so CMP_LT is 1 | Pass |

Register loading was also checked during the first addition test.

## What the results mean

These tests check common operations and a few important edge cases. They do not cover every possible input combination. All 21 tests were rerun and passed on the final straight-wire MUX layout with the corrected shift settings.
