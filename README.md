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

  ```
- `spike pk`: RISC-V ISA simulator.
- ```bash

  ```
- Shell scripting: For setting environment variables and embedding unique IDs.
- ```bash
  export U=$(id -un)
export H=$(hostname -s)
export M=$(cat /etc/machine-id | head -c 16)
export T=$(date -u +%Y-%m-%dT%H:%M:%SZ)
export E=$(date +%s)```

# output
Using built-in specs.
COLLECT_GCC=riscv64-unknown-elf-gcc
COLLECT_LTO_WRAPPER=/home/himanshu/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin/../libexec/gcc/riscv64-unknown-elf/8.3.0/lto-wrapper
Target: riscv64-unknown-elf
Configured with: /scratch/carsteng/freedom-tools-master/obj/x86_64-linux-ubuntu14/build/riscv-gnu-toolchain/riscv-gcc/configure --target=riscv64-unknown-elf --host=x86_64-linux-gnu --prefix=/scratch/carsteng/freedom-tools-master/obj/x86_64-linux-ubuntu14/install/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14 --with-pkgversion='SiFive GCC 8.3.0-2019.08.0' --with-bugurl=https://github.com/sifive/freedom-tools/issues --disable-shared --disable-threads --enable-languages=c,c++ --enable-tls --with-newlib --with-sysroot=/scratch/carsteng/freedom-tools-master/obj/x86_64-linux-ubuntu14/install/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf --with-native-system-header-dir=/include --disable-libmudflap --disable-libssp --disable-libquadmath --disable-libgomp --disable-nls --disable-tm-clone-registry --src=../riscv-gcc --without-system-zlib --enable-checking=yes --enable-multilib --with-abi=lp64d --with-arch=rv64imafdc CFLAGS=-O2 CXXFLAGS=-O2 'CFLAGS_FOR_TARGET=-Os  -mcmodel=medany' 'CXXFLAGS_FOR_TARGET=-Os  -mcmodel=medany'
Thread model: single
__gcc version 8.3.0 (SiFive GCC 8.3.0-2019.08.0)__ 


### Program List
- Each program contains unique as header.
1. **factorial.c** – Computes factorial of a fixed number.
2. **max_array.c** – Finds the maximum value in an integer array.
3. **bitops.c** – Performs bitwise AND, OR, XOR, shifts.
4. **bubble_sort.c** – Sorts an array using bubble sort.

---



`
