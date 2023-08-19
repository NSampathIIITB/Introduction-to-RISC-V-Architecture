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
<br>
The **RISC-V** (pronounced "risk-five") Instruction Set Architecture (ISA) is a specification that defines the instructions and their encoding formats for processors that adhere to the RISC-V architecture. The RISC-V ISA is designed to be modular, extensible, and customizable, allowing for a wide range of implementations tailored to various application domains. The ISA is defined by a series of standard documents that describe the instructions, memory model, exception handling, and other architectural features.
</br>
<br> 
The term "ISA" stands for "Instruction Set Architecture." It refers to the set of instructions that a microprocessor or computer architecture understands and can execute. The ISA defines the machine-level programming model, including the available instructions, their encoding formats, the registers they can operate on, memory addressing modes, and how instructions interact with the hardware. In essence, the ISA serves as an interface between software and hardware, enabling software developers to write programs that can run on a specific microprocessor or computer architecture.</br>

<br>
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

The RISC-V ISA specification documents provide detailed information about each instruction, its encoding, its behavior, and its interaction with other instructions and architectural features. The open and modular nature of the RISC-V ISA has led to its widespread adoption in various industries, from embedded systems to high-performance computing.<br>

Each base integer set is characterized by the width of the register (XLEN) and size of the user address space. The most important advantage of RISC-V is that it is an open standard instruction which is easily available for academics and commercial purposes free of cost.

The detail of the RISC-V instructions set manual can be found [here](https://riscv.org/wp-content/uploads/2017/05/riscv-spec-v2.2.pdf).

</details>

<details>
 
  <summary> GNU compile toolchain</summary>
<br>
  The GNU compile toolchain is a set of programming tools in LINUX system that can be use for compiling a code to generate certain executable program, library and debugger and whose detail can be found in references. RISC-V is one such toolchain which supports C and C++ cross compiler. It supports two build modes: a generic ELF/Newlib toolchain and a more sophisticated Linux-ELF/glibc toolchain and the github link for the same can be found in references. 

1. Compiler and linker which transform the source code into an executable program.
2. Libraries which provide interfaces to the operating system.
3. Debugger which is used to test and debug created program.
4. the output of the compiler completely depends on the hardware.
   

To start off a c program to compile sum from 1 to n was written whose  codes given below as [sum1ton.c]

```

#include<stdio.h>
int main()
{
   int i,sum=0,n=100;
   
   for(i=1;i<=n;i++)
      {
        sum=sum+i;
       }
   printf(" sum of numbers from 1 to n is %d, n is %d \n",sum,n);
}

```

In case RISC-V GNU toolchain the follwing commands are executed

**To use the RISC-V gcc compiler or simulator**

    `riscv64-unknown-elf-gcc <compiler option -O1 ; Ofast> -mabi=lp64  -march=rv64i  -o <object filename.o> <Cfilename.c>`

   Here -01 gives 15 instructions set while -0fast gives us 12 instructions set
    
**To list the details of a file**
  
  ```
ls -ltr <filename.o>

```

![Screenshot from 2023-08-19 18-48-08](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/7b175af7-6dc7-49c1-91cb-69ae9cd20e04)

**To disassemble the object file**

```

riscv64-unknown-elf-objdump  -d  <object filename.o> (or)
riscv64-unknown-elf-objdump  -d <object filename.o> | less

```
![Screenshot from 2023-08-19 18-54-04](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/eb9e760c-a32d-42e0-8518-9d16072517c2)

```
/main
n

```
This code helps in seeing the **main** in exe file:

![Screenshot from 2023-08-19 18-55-53](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/8e32ec57-7ee8-436c-b77e-751bcb27597e)

here we can check the instruction set is 15 by subtracting  10214-101ac = 58\4=15 instruction sets 

**To compile:**

```
spike pk <object filename.o>
```
![Screenshot from 2023-08-19 19-00-06](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/cfae0116-8a0b-4f72-b47a-b8fc49d2d100)

**To debug using spike:**

```
spike -d pk <object filename.o>
```
![Screenshot from 2023-08-19 19-04-03](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/b363049a-362c-460e-9019-98eca71c5c64)

After running the above code line a number of things can be done as demonstrated in the image below. The code can be manually debugged, part of it can be run and contents of registers can be checked.

we can use these commands in spike while debugging
```
(spike): until pc 0 <desired address>  //To move the pc to desired address
(spike): reg 0 a0                      //To found the contents in a0
(spike): click enter                   //To run the next instruction
(spike): q                             //To exit spike

````
![Screenshot from 2023-08-19 19-14-55](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/57b9edb6-e6ea-4049-94c9-5169ff2d907c)

  </details>

  



[Acknowledgement](#acknowledgement)

[Reference](#reference)


