# Commodore Assembly

Educational 6502 assembly programming for Commodore 8-bit computers.

This repository contains a collection of assembly language programs and reusable routines intended to explore programming on the classic Commodore machines. The emphasis is on understanding how the 6502 processor works, learning assembly programming techniques, and building useful routines from the ground up.

## Supported architectures

The code is designed to be as architecture-independent as practical, supporting:

- **Commodore PET**
- **Commodore VIC-20**
- **Commodore 64**

The machines share a common 6502 instruction set, but differ in memory layout, ROM routines and hardware. This project aims to keep the actual assembly routines reusable across all three architectures, isolating machine-specific differences where necessary.

The target architecture is selected through the `ARCH` assembler variable in `main.a`:

```asm
ARCH="C64"       ; "C64", "VIC20" or "PET"
```

For the VIC-20, the `VIC20_RAM` variable specifies the memory expansion:

```asm
VIC20_RAM=0      ; 0, 3, 8, 16 or 24 KB expansion
```

The BASIC startup code in `basic.a` uses these settings to select the appropriate BASIC program start address and generate the BASIC `SYS` statement that launches the assembly program.

The code uses the common 6502 instruction set (`!cpu 6502`), so it can be assembled for all three machines without changing the processor instruction set.

## Repository contents

| File | Description |
|---|---|
| `main.a` | Main program and architecture selection |
| `basic.a` | BASIC startup stub, including the `SYS` call to the assembly program |
| `common.a` | Common hardware definitions, constants and shared declarations |
| `strgio.a` | String input/output routines |
| `atoi.a` | ASCII/PETSCII decimal string to integer conversion |
| `hello_world.a` | Hello World example |

The routines are intended to be reusable: programs can include the required source files and call the routines they need.

## Getting started

### Requirements

You need two tools:

- **[ACME](https://sourceforge.net/projects/acme-crossass/)** – a cross-assembler for 6502-family processors.
- **[VICE](https://vice-emu.sourceforge.io/)** – an emulator for Commodore 8-bit computers.

Both are available for Linux and other platforms.

### 1. Get the source code

Clone the repository:

```sh
git clone https://github.com/schur/Commodore-assembly.git
cd Commodore-assembly
```

### 2. Select the target architecture

Open `main.a` and set the `ARCH` variable to the machine you want to target.

For example, for the Commodore 64:

```asm
ARCH="C64"
```

For a VIC-20, also set the appropriate memory expansion:

```asm
ARCH="VIC20"
VIC20_RAM=0
```

For a PET:

```asm
ARCH="PET"
```

### 3. Assemble the program

Run ACME from the repository directory:

```sh
acme main.a
```

The output filename is specified in `main.a` using the `!to` directive. The default output is:

```text
main.prg
```

### 4. Run the program in VICE

Start the appropriate VICE emulator with the generated program.

**Commodore 64:**

```sh
x64sc -autostart main.prg
```

**VIC-20:**

```sh
xvic -autostart main.prg
```

**Commodore PET:**

```sh
xpet -autostart main.prg
```

Depending on your VICE installation, the emulator executable names may differ. For example, some installations provide `x64` instead of `x64sc`.

## Learning and experimentation

The routines in this repository are intended as educational examples rather than a finished software library. They are developed incrementally, with an emphasis on readable assembly code, reusable interfaces and an understanding of the underlying hardware.

The architecture-independent approach is particularly useful for comparing how similar programs behave on the PET, VIC-20 and C64, while keeping most of the assembly code unchanged.

Contributions, suggestions and improvements are welcome.
