# Buffer Overflow Attack — CS442 Software Security

Lab assignment for **CS442: Software Security**, College of Computer and Information Sciences, Imam Mohammad Ibn Saud Islamic University (First Semester 2025-2026).

## Overview

This assignment demonstrates a classic **stack buffer overflow** attack, where crafted input overwrites a saved return address to redirect program execution into injected shellcode, gaining a root shell on a set-UID program.

## Steps

### Task One: Modify exploit.py

1. Disabled address space layout randomization (ASLR) for stable addresses.
2. Compiled the vulnerable program, set it as set-UID root, and created the initial `badfile`.
3. Used GDB to locate the vulnerable function, set a breakpoint, and found the offset between the stack base pointer (`$ebp`) and the buffer (631 bytes).
4. Built the exploit payload: a NOP sled, shellcode placed near the end of the buffer, and the crafted return address written at the correct offset.
5. Generated the final `badfile` and confirmed the exploit worked, spawning a shell as the program's privileged user.

### Task Two: Obtain a root shell

1. Modified the exploit to spawn a different shell instead of the default one.
2. Rebuilt `badfile` and re-ran the exploit.
3. Verified a root shell was obtained (`euid=0`).

### Task Three: Defeat address randomization

1. Re-enabled ASLR to make exploitation harder.
2. Ran a brute-force loop that repeatedly attempted the exploit, tracking elapsed time and attempt count.
3. After repeated attempts (~25 minutes), the randomized address was guessed and the exploit succeeded.

## Environment

- GDB for debugging and memory inspection
- A vulnerable set-UID C program with a stack buffer overflow
- Python exploit script (`exploit.py`)

## Note

This exploit was built and run in an isolated lab environment for educational purposes, as part of a university course on software security.
