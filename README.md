# RISC-V-Architecture

This github repository summarizes the progress made in the ASIC class about RISC-V Architecture . Quick links:

[Day-0 : Installation of RISC-V toolchain](#day-0)

[Day-1 : Introduction to RISC-V ISA And GNU compiler toolchain](#day-1)

[Day-2 : Introduction to Application Binary Interface And Basic Error Flow](#day-2)

[Day-3 : Digital Logic with TL-Verilog and Makerchip](#day-3)

[Day-4 : Basic RISC-V CPU micro-architecture](#day-4)

[Day-5 : Complete Pipelined RISC-V CPU micro-architecture](#day-5)

## Day-0

<details> 
<summary> Installation </summary>
 
**Steps to install RISC-V toolchain**

```
git clone https://github.com/kunalg123/riscv_workshop_collaterals.git
cd riscv_workshop_collaterals
chmod +x run.sh
./run.sh

```

 Once you run it you will get **make** error. ignore it  and type the following commands

 ```

cd ~/riscv_toolchain/iverilog/
git checkout --track -b v10-branch origin/v10-branch
git pull 
chmod 777 autoconf.sh 
./autoconf.sh 
./configure 
make
sudo make install

```

- To set the PATH variable in .bashrc

```
source .bashrc
gedit .bashrc
#Instead of **nsaisampath** put your **username**
export PATH="/home/nsaisampath/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH" #Type at last line # save and close the bashrc and type
source .bashrc

```
</details>

## Day-1

<details>
<summary> Introduction to RISC-V ISA </summary>
</br>
The **RISC-V** (pronounced "risk-five") Instruction Set Architecture (ISA) is a specification that defines the instructions and their encoding formats for processors that adhere to the RISC-V architecture. The RISC-V ISA is designed to be modular, extensible, and customizable, allowing for a wide range of implementations tailored to various application domains. The ISA is defined by a series of standard documents that describe the instructions, memory model, exception handling, and other architectural features.
</br>
 
The term "ISA" stands for "Instruction Set Architecture." It refers to the set of instructions that a microprocessor or computer architecture understands and can execute. The ISA defines the machine-level programming model, including the available instructions, their encoding formats, the registers they can operate on, memory addressing modes, and how instructions interact with the hardware. In essence, the ISA serves as an interface between software and hardware, enabling software developers to write programs that can run on a specific microprocessor or computer architecture.

The base RISC-V instruction set is divided into several standard "base" integer instruction set variants, labeled as RV32I, RV64I, and RV128I, depending on the word size. Here's a brief overview of the base integer instruction sets:

1. **RV32I:** This is the 32-bit base integer instruction set. It includes a set of instructions for integer arithmetic, logic operations, data movement, branching, and bit manipulation. Instructions are encoded in 32 bits.

2. **RV64I:** This is the 64-bit base integer instruction set. It is an extension of RV32I, offering the same set of instructions but designed for a 64-bit word size.

3. **RV128I:** This is the 128-bit base integer instruction set, extending the capabilities of RV64I to a 128-bit word size.

In addition to the base integer instruction sets, RISC-V also supports various extension modules that can be added to the base instruction set to enhance the processor's capabilities. Some of the common extension modules include:

- **M:** Integer multiplication and division instructions.
- **A:** Atomic memory access instructions for multi-threaded and multi-processor systems.
- **F:** Single-precision floating-point arithmetic instructions.
- **D:** Double-precision floating-point arithmetic instructions.
- **C:** Compressed instructions for reduced code size.
- **V:** Vector processing instructions for SIMD operations.
- **B:** Bit manipulation instructions.

These extension modules can be mixed and matched based on the requirements of the target application, allowing for customization and specialization of the processor architecture.

RISC-V also defines different privilege levels (User, Supervisor, Machine) that dictate the level of access to resources and control over the system. This hierarchy of privilege levels is designed to support various software layers, from application code to operating systems.

The RISC-V ISA specification documents provide detailed information about each instruction, its encoding, its behavior, and its interaction with other instructions and architectural features. The open and modular nature of the RISC-V ISA has led to its widespread adoption in various industries, from embedded systems to high-performance computing.

The detail of the RISC-V instructions set manual can be found [here](https://riscv.org/wp-content/uploads/2017/05/riscv-spec-v2.2.pdf).

**These below images gives a basic idea about how the RISC-V architecture is used in general**
![Screenshot from 2023-08-17 20-19-14](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/7d1b019f-c9dd-4aec-b313-adc0c47114f1)
![Screenshot from 2023-08-17 20-24-09](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/a3f98b27-183d-4434-851b-ebd82cdb7ec0)
![Screenshot from 2023-08-17 20-27-14](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/6a4ccb69-a86c-4e7c-bed5-a0d34860a837)



</details>


[Acknowledgement](#acknowledgement)

[Reference](#reference)


