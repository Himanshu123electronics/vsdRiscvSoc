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
  riscv64-unknown-elf-gcc -O0 -S factorial.c -o factorial.s
  ```
  
- `spike pk`: RISC-V ISA simulator.
- ```bash
  spike --helo
  ```
   
  
- Shell scripting: For setting environment variables and embedding unique IDs.
- ```bash
  export U=$(id -un)
  export H=$(hostname -s)
  export M=$(cat /etc/machine-id | head -c 16)
  export T=$(date -u +%Y-%m-%dT%H:%M:%SZ)
  export E=$(date +%s)
  
# ouput 
```bash
Using built-in specs.
COLLECT_GCC=riscv64-unknown-elf-gcc
COLLECT_LTO_WRAPPER=/home/himanshu/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin/../libexec/gcc/riscv64-unknown-elf/8.3.0/lto-wrapper
Target: riscv64-unknown-elf
Configured with: /scratch/carsteng/freedom-tools-master/obj/x86_64-linux-ubuntu14/build/riscv-gnu-toolchain/riscv-gcc/configure --target=riscv64-unknown-elf --host=x86_64-linux-gnu --prefix=/scratch/carsteng/freedom-tools-master/obj/x86_64-linux-ubuntu14/install/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14 --with-pkgversion='SiFive GCC 8.3.0-2019.08.0' --with-bugurl=https://github.com/sifive/freedom-tools/issues --disable-shared --disable-threads --enable-languages=c,c++ --enable-tls --with-newlib --with-sysroot=/scratch/carsteng/freedom-tools-master/obj/x86_64-linux-ubuntu14/install/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf --with-native-system-header-dir=/include --disable-libmudflap --disable-libssp --disable-libquadmath --disable-libgomp --disable-nls --disable-tm-clone-registry --src=../riscv-gcc --without-system-zlib --enable-checking=yes --enable-multilib --with-abi=lp64d --with-arch=rv64imafdc CFLAGS=-O2 CXXFLAGS=-O2 'CFLAGS_FOR_TARGET=-Os  -mcmodel=medany' 'CXXFLAGS_FOR_TARGET=-Os  -mcmodel=medany'
Thread model: single
gcc version 8.3.0 (SiFive GCC 8.3.0-2019.08.0)
```
# Unique.h file
```bash
#ifndef UNIQUE_H
#define UNIQUE_H

#include <stdio.h>
#include <stdint.h>
#include <time.h>

#ifndef USERNAME
#define USERNAME "unknown_user"
#endif

#ifndef HOSTNAME
#define HOSTNAME "unknown_host"
#endif

#ifndef MACHINE_ID
#define MACHINE_ID "unknown_machine"
#endif

#ifndef BUILD_UTC
#define BUILD_UTC "unknown_time"
#endif

#ifndef BUILD_EPOCH
#define BUILD_EPOCH 0
#endif

static uint64_t fnv1a64(const char *s) {
    const uint64_t OFF = 1469598103934665603ULL;
    const uint64_t PRIME = 1099511628211ULL;
    uint64_t h = OFF;
    for (const unsigned char *p = (const unsigned char *)s; *p; ++p) {
        h ^= *p;
        h *= PRIME;
    }
    return h;
}

static void uniq_print_header(const char *program_name) {
    time_t now = time(NULL);
    char buf[512];
    int n = snprintf(
        buf, sizeof(buf), "%s|%s|%s|%s|%ld|%s|%s",
        USERNAME, HOSTNAME, MACHINE_ID, BUILD_UTC,
        (long)BUILD_EPOCH, __VERSION__, program_name
    );
    (void)n;

    uint64_t proof = fnv1a64(buf);

    char rbuf[600];
    snprintf(rbuf, sizeof(rbuf), "%s|run_epoch=%ld", buf, (long)now);
    uint64_t runid = fnv1a64(rbuf);

    printf("=== RISC-V Proof Header ===\n");
    printf("User        : %s\n", USERNAME);
    printf("Host        : %s\n", HOSTNAME);
    printf("MachineID   : %s\n", MACHINE_ID);
    printf("BuildUTC    : %s\n", BUILD_UTC);
    printf("BuildEpoch  : %ld\n", (long)BUILD_EPOCH);
    printf("GCC         : %s\n", __VERSION__);
    printf("PointerBits : %d\n", (int)(8 * (int)sizeof(void *)));
    printf("Program     : %s\n", program_name);
    printf("ProofID     : 0x%016llx\n", (unsigned long long)proof);
    printf("RunID       : 0x%016llx\n", (unsigned long long)runid);
    printf("===========================\n");
}

#endif // UNIQUE_H
```

### Program List
- Each program contains unique as header.
1. **factorial.c** – Computes factorial of a fixed number.
2. **max_array.c** – Finds the maximum value in an integer array.
3. **bitops.c** – Performs bitwise AND, OR, XOR, shifts.
4. **bubble_sort.c** – Sorts an array using bubble sort.

---


## Compile factorial.c

```bash
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
factorial.c -o factorial
```


## Compile max_array.c

```bash
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
array.c -o array
```


## Compile bitops.c

```bash
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bitops.c -o bitops
```


## Compile bubble_sort.c

```bash
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bubble_sort.c -o bubble_sort
```

 ## Run factorial.c

```bash
spike ~/riscv_toolchain/riscv-pk/build/pk ./factorial
```


## Run max_array.c

```bash
spike ~/riscv_toolchain/riscv-pk/build/pk ./array
```


## Run bitops.c

```bash
spike ~/riscv_toolchain/riscv-pk/build/pk ./bitops
```


## Run bubble_sort.c

```bash
spike ~/riscv_toolchain/riscv-pk/build/pk ./bubble_sort
```

## Assemble factorial.s

```bash
riscv64-unknown-elf-gcc -O0 -S factorial.c -o factorial.s
```


## Assemble array.s

```bash
riscv64-unknown-elf-gcc -O0 -S max_array.c -o array.s
```


## Assemble bitops.s

```bash
riscv64-unknown-elf-gcc -O0 -S bitops.c -o bitops.s
```


## Assemble bubble_sort.s

```bash
riscv64-unknown-elf-gcc -O0 -S bubble_sort.c -o bubble_sort.s
```



## Disassembly of factorial
```bash
riscv64-unknown-elf-objdump -d ./factorial | sed -n '/<main>:/,/^$/p' | tee factorial_main_objdump.txt
```


## Disassembly of array
```bash
riscv64-unknown-elf-objdump -d ./array | sed -n '/<main>:/,/^$/p' | tee max_array_main_objdump.txt
```


## Disassembly of bitops
```bash
riscv64-unknown-elf-objdump -d ./bitops | sed -n '/<main>:/,/^$/p' | tee bitops_main_objdump.txt
```


## Disassembly of bubble_sort
```bash
riscv64-unknown-elf-objdump -d ./bubble_sort | sed -n '/<main>:/,/^$/p' | tee bubble_sort_main_objdump.txt
```

