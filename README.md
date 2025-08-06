# Task 2:RISC-V Setup Check

This repository demonstrates a working RISC-V toolchain by compiling and executing RISC-V C programs locally, generating outputs, and manually decoding instructions. The goal is to verify that the build and execution process is unique to the user's system.

---

## Objective

- Run 4 RISC-V C programs on your local machine.
- Compile them using RISC-V toolchain (`riscv64-unknown-elf-gcc`).
- Execute them using `spike pk`.
- Include unique identifiers from PC in the output using a custom header.
- Generate assembly (`.s`) and disassembly (`objdump`) for each.
- Manually decode at least 5 RISC-V integer instructions.

---

## Tools Used

- `riscv64-unknown-elf-gcc`: For compiling RISC-V programs.
- ```bash

  
- `spike pk`: RISC-V ISA simulator.
- ```bash

  
- Shell scripting: For setting environment variables and embedding unique IDs.
- ```bash
  export U=$(id -un)
export H=$(hostname -s)
export M=$(cat /etc/machine-id | head -c 16)
export T=$(date -u +%Y-%m-%dT%H:%M:%SZ)
export E=$(date +%s)




### Program List
- Each program contains unique as header.
1. **factorial.c** – Computes factorial of a fixed number.
2. **max_array.c** – Finds the maximum value in an integer array.
3. **bitops.c** – Performs bitwise AND, OR, XOR, shifts.
4. **bubble_sort.c** – Sorts an array using bubble sort.

---



`
