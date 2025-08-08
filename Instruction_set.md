| Instruction | Type | Opcode | rd | funct3 | rs1 | rs2 | funct7 | Binary Immediate | Description |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| `addi sp, sp, -64` | I-Type | `0010011` | `x2` | `000` | `x2` | N/A | N/A | `111111000000` | $x2 = x2 + (-64)$ |
| `sd ra, 56(sp)` | S-Type | `0100011` | N/A | `011` | `x2` | `x1` | N/A | `imm[11:5]=0011100`<br>`imm[4:0]=10000` | $Memory[x2 + 56] = x1$ |
| `sd s0, 48(sp)` | S-Type | `0100011` | N/A | `011` | `x2` | `x8` | N/A | `imm[11:5]=0011000`<br>`imm[4:0]=10000` | $Memory[x2 + 48] = x8$ |
| `addi s0, sp, 64` | I-Type | `0010011` | `x8` | `000` | `x2` | N/A | N/A | `000001000000` | $x8 = x2 + 64$ |
| `lui a5, 0x1d` | U-Type | `0110111` | `x15`| N/A | N/A | N/A | N/A | `00000000000111010000` | $x15 = 0x1d \ll 12$ |


| Instruction | Type | Opcode | rd | funct3 | rs1 | rs2 | funct7 | Binary Immediate | Description |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| `addi sp, sp, -64` | I-Type | `0010011` | `x2` | `000` | `x2` | N/A | N/A | `111111000000` | $x2 = x2 + (-64)$ |
| `sd ra, 56(sp)` | S-Type | `0100011` | N/A | `011` | `x2` | `x1` | N/A | `imm[11:5]=0011100`<br>`imm[4:0]=10000` | $Memory[x2 + 56] = x1$ |
| `sd s0, 48(sp)` | S-Type | `0100011` | N/A | `011` | `x2` | `x8` | N/A | `imm[11:5]=0011000`<br>`imm[4:0]=10000` | $Memory[x2 + 48] = x8$ |
| `addi s0, sp, 64` | I-Type | `0010011` | `x8` | `000` | `x2` | N/A | N/A | `000001000000` | $x8 = x2 + 64$ |
| `lui a5, 0x1c` | U-Type | `0110111` | `x15`| N/A | N/A | N/A | N/A | `0000000000011100` | $x15 = 0x1c \ll 12$ |

| Instruction | Type | Opcode | rd | funct3 | rs1 | rs2 | funct7 | Binary Immediate | Description |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| `addi sp, sp, -32` | I-Type | `0010011` | `x2` | `000` | `x2` | N/A | N/A | `11111100000` | $x2 = x2 + (-32)$ |
| `sd ra, 24(sp)` | S-Type | `0100011` | N/A | `011` | `x2` | `x1` | N/A | `imm[11:5]=0001100`<br>`imm[4:0]=01000` | $Memory[x2 + 24] = x1$ |
| `sd s0, 16(sp)` | S-Type | `0100011` | N/A | `011` | `x2` | `x8` | N/A | `imm[11:5]=0001000`<br>`imm[4:0]=00000` | $Memory[x2 + 16] = x8$ |
| `addi s0, sp, 32` | I-Type | `0010011` | `x8` | `000` | `x2` | N/A | N/A | `000000100000` | $x8 = x2 + 32$ |
| `lui a5, 0x1c` | U-Type | `0110111` | `x15`| N/A | N/A | N/A | N/A | `0000000000011100` | $x15 = 0x1c \ll 12$ |

| Instruction | Type | Opcode | rd | funct3 | rs1 | rs2 | funct7 | Binary Immediate | Description |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| `jal ra, 101ce` | J-Type | `1101111` | `x1` | N/A | N/A | N/A | N/A | `11011100010111111111` | $ra = pc + 4; pc = pc - 0x23c$ |
| `lui a5, 0x1d` | U-Type | `0110111` | `x15`| N/A | N/A | N/A | N/A | `0000000000011101` | $x15 = 0x1d \ll 12$ |
| `addi a5, a5, -1880` | I-Type | `0010011` | `x15` | `000` | `x15` | N/A | N/A | `100010101000` | $x15 = x15 + (-1880)$ |
| `ld a1, 0(a5)` | I-Type | `0000011` | `x11` | `011` | `x15` | N/A | N/A | `000000000000` | $x11 = Memory[x15 + 0]$ |
| `ld a2, 8(a5)` | I-Type | `0000011` | `x12` | `011` | `x15` | N/A | N/A | `000000001000` | $x12 = Memory[x15 + 8]$ |
