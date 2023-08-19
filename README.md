# RISC-V-Architecture

This github repository summarizes the progress made in the ASIC class about RISC-V Architecture . Quick links:

[Day-0 : Installation of RISC-V toolchain](#day-0)

[Day-1 : Introduction to RISC-V ISA And GNU compiler toolchain](#day-1)

[Day-2 : Introduction to Application Binary Interface And Basic Error Flow](#day-2)

[Day-3 : Digital Logic with TL-Verilog and Makerchip](#day-3)

[Day-4 : Basic RISC-V CPU micro-architecture](#day-4)

[Day-5 : Complete Pipelined RISC-V CPU micro-architecture](#day-5)

[Acknowledgement](#acknowledgement)

[Reference](#reference)


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
<details>
 <summary> Integer number Representation </summary>
 <br>
 The RISC-V architecture defines several different data types and number systems to represent and manipulate data. Here, I'll explain the basic number systems used in RISC-V:

- **Binary Number System**: RISC-V, like most digital systems, primarily operates on binary data. In the binary number system, numbers are represented using only two symbols: 0 and 1. Each digit in a binary number represents a power of 2. For example, the binary number "1101" represents (1 * 2^3) + (1 * 2^2) + (0 * 2^1) + (1 * 2^0) = 13 in decimal.
- **Integer Representation**: RISC-V supports different integer data types with varying sizes. The most common are 32-bit and 64-bit integers, denoted as "RV32" and "RV64" respectively. Integers are typically represented in two's complement form, which allows both positive and negative values to be stored and manipulated using the same hardware.
- **Floating-Point Representation**: RISC-V also supports floating-point operations for real numbers. Floating-point numbers are represented using a sign bit, an exponent, and a fraction (also known as mantissa). RISC-V defines different formats for floating-point numbers, including the IEEE 754 standard formats (single precision, double precision, etc.). These formats allow a wide range of values to be represented with varying levels of precision.
- **Hexadecimal Notation**: While binary is the fundamental representation in RISC-V, hexadecimal (base-16) notation is often used to represent binary numbers in a more human-readable form. Each hexadecimal digit represents four bits. For example, the binary number "11011010" can be represented as "DA" in hexadecimal.
- **Memory Addressing**: RISC-V CPUs use memory addresses to access data stored in memory. Memory addresses are typically represented in hexadecimal form. The exact memory addressing scheme depends on the specific RISC-V implementation and the memory model being used.
Overall, the RISC-V architecture provides a flexible framework for representing and manipulating different types of numbers, allowing software developers and hardware designers to efficiently perform arithmetic and logical operations on various data types within the context of RISC-V-based systems.

In computer architecture, the terms "bit," "byte," "word," and "double word" refer to different units of data storage and manipulation. These terms are used to describe the size of data that a computer's memory and processing units can handle. The specific sizes of these units can vary based on the architecture and implementation, but I'll provide you with some common interpretations:

- **Bit**: A bit is the smallest unit of data in computing. It can represent one of two values: 0 or 1. Bits are the building blocks of all digital information and are used to represent various types of data and instructions in a computer's memory and processing units.
- **Byte**: A byte is a group of 8 bits. It is the basic addressable unit of memory storage in most computer architectures. Bytes are commonly used to represent characters, numbers, and other small data elements. For example, the ASCII code for the letter 'A' is 65, which can be represented as a byte with the binary value 01000001.
- **Word**: The term "word" refers to the natural data size that a computer's central processing unit (CPU) can process in a single operation. The size of a word can vary between different computer architectures. In the context of x86 and x86-64 architectures, a word is typically 16 bits, while in other architectures like RISC-V, a word can be 32 bits or 64 bits. The size of a word determines the maximum amount of data that the CPU can manipulate at once, which can impact the efficiency of data processing.
- **Double Word (Dword)**: The term "double word" (often abbreviated as "dword") is used to describe a data unit that is twice the size of a standard word. In x86 and x86-64 architectures, a double word is 32 bits, while in some other architectures, it can refer to a 64-bit value. The term "dword" is often used in the x86 family of processors to describe a 32-bit data value.
It's important to note that the exact sizes of these units can vary based on the computer architecture and implementation.

**64-bit Unsigned Numbers:**

A 64-bit unsigned number, often referred to as a "64-bit unsigned integer," is a data type commonly used in computer programming and digital systems. It represents a non-negative whole number within the range of 0 to 18,446,744,073,709,551,615 i.e 0 to 2^64-1.

Here's a breakdown of its properties:

- **Bit Length**: A 64-bit number consists of 64 binary digits (bits), which can be either 0 or 1.

- **Range**: As mentioned earlier, the range of values a 64-bit unsigned number can represent is from 0 to 18,446,744,073,709,551,615. This is because you have 2^64 possible combinations of bits, starting from all bits being 0 (representing 0) to all bits being 1 (representing 2^64 - 1).

- **Memory**: In memory, a 64-bit unsigned number occupies exactly 8 bytes (64 bits / 8 bits per byte), which is 64 / 8 = 8 bytes.

- **Data Representation**: These numbers are often represented in various numeral systems, including binary, decimal, hexadecimal, and octal. In binary, a 64-bit unsigned number is represented using 64 binary digits (0s and 1s), in decimal using regular base-10 numerals, in hexadecimal using base-16 digits (0-9, A-F), and in octal using base-8 digits (0-7).

- **Usage**: 64-bit unsigned numbers are commonly used in various applications such as computer programming, data storage, cryptography, and more. They provide a large range of values while avoiding the complications associated with signed numbers, which have both positive and negative values.

Here's an example representation of the maximum 64-bit unsigned number in various numeral systems:
```
- Binary: 1111111111111111111111111111111111111111111111111111111111111111
- Decimal: 18,446,744,073,709,551,615
- Hexadecimal: FFFFFFFF FFFFFFFF
- Octal: 1777777777777777777777
```
Keep in mind that when working with these numbers in programming languages, you might encounter specific syntax or functions to handle them appropriately. Different programming languages might have different ways of representing and manipulating 64-bit unsigned numbers.

**64-bit Signed Numbers:**

A 64-bit signed number is a data type used to represent both positive and negative whole numbers within a range using 64 binary digits (bits). The most common representation used for signed numbers is the two's complement representation. Here are the key characteristics of 64-bit signed numbers:

- **Bit Length**: A 64-bit signed number consists of 64 binary digits (bits), which can be either 0 or 1.

- **Range**: In the two's complement representation, a 64-bit signed number can represent values from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 i.e -2^63 to 2^63-1 . The range covers both negative and positive values.

- **Memory**: In memory, a 64-bit signed number occupies exactly 8 bytes (64 bits / 8 bits per byte).

- **Representation**: In the two's complement representation, the most significant bit (MSB), which is the leftmost bit, represents the sign of the number. If the MSB is 0, the number is positive. If the MSB is 1, the number is negative. The remaining bits represent the magnitude of the number in binary form.

- **Usage**: 64-bit signed numbers are used in various applications, including computer programming, data storage, scientific computations, and more. They provide a wide range of values that can be used for many different purposes.

Here's an example representation of the maximum and minimum 64-bit signed numbers in binary:

- Maximum (positive): 0111111111111111111111111111111111111111111111111111111111111111
- Minimum (negative): 1000000000000000000000000000000000000000000000000000000000000000

Keep in mind that when working with these numbers in programming languages, you might encounter specific syntax or functions to handle them appropriately. Different programming languages might have different ways of representing and manipulating 64-bit signed numbers.

![Screenshot from 2023-08-19 10-48-29](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/c227568f-07db-47b9-8b79-e6bf1e54a2bc)

 
</details>  





<details>
<summary> Lab for Unsigned and Signed numbers </summary>
 
**Code for unsignedHighest:**

```
#include <stdio.h>
#include <math.h>
int main() {
unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
printf("highest number represented by unsigned long long int is %llu\n", max);
return 0;
}

```

![Screenshot from 2023-08-19 21-36-18](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/a5193fca-218e-4cca-9da2-7c5c9156b088)


This show the Highest value for Unsigned Numbers
if we change the code to get the lowest value for Unsigned Number by changing **(pow(2,64) -1) to( pow(2,10)*-1)**;

![Screenshot from 2023-08-19 21-40-00](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/c535e1be-0b3d-43c6-9067-e1f1ea7577c1)

**Code for signed Numbers:**

```
#include <stdio.h>
#include <math.h>
int main(){
long long int max = (long long int) (pow(2,10) * -1);
printf("highest number represented by long long int is %lld\n", max);
return 0;
}

```

![Screenshot from 2023-08-19 21-43-09](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/7bc371e9-c9fd-4c67-af16-88fcacabd2f6)


**Example-1**

code:

```
#include <stdio.h>
#include <math.h>
int main() {
long long int max = (int) (pow(2,63) -1);
long long int min = (int) (pow(2,63) * -1);
printf("highest number represented by long long int is %lld\n", max);
printf("lowest number represented by long long int is %lld\n", min);
return 0;

```
![Screenshot from 2023-08-19 11-35-52](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/f79a69eb-6ee1-4aa9-b53c-b5360032453b)

Here in this code we have to change :

```
long long int max = (long long int) (pow(2,63) -1);
long long int min = (long long int) (pow(2,63) * -1);

```
so corrected output :

![Screenshot from 2023-08-19 21-43-09](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/7bc371e9-c9fd-4c67-af16-88fcacabd2f6)

Table : 

![Screenshot from 2023-08-19 11-37-23](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/9b4bbf62-7aba-4463-b56b-2579328f9555)

**LAB WORK**

**1.For the C program used in labs, use a value of n=9, compile and simulate using gcc compiler. What is the output you get?**

![Screenshot from 2023-08-19 21-58-10](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/19830ea5-a6ac-451c-b380-f569c63944df)

**2.As shown in labs, compile the C program (n=9) using riscv-gcc compiler with O1 switch and look at assembly code using riscv-objdmp. What is the memory location of "printf" subroutine ?**

![Screenshot from 2023-08-19 22-00-07](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/e43843b7-faef-45f1-81d8-0c6d43358154)

**3.How many instructions are used in "printf" subroutine for C program (n=9) compiled with riscv-gcc and O1 switch?**

![Screenshot from 2023-08-19 22-04-52](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/100df588-3067-43da-a010-92ee03359ee2)

**4.As shown in labs, compile the C program (n=9) using riscv-gcc compiler with Ofast switch and look at assembly code using riscv-objdmp. How many instructions are used by "main" program ?**

![Screenshot from 2023-08-19 22-08-46](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/1e05dc3e-8534-4f8f-8c93-3a64dded24b2)

**5.Debug C program (n=9) with spike and run until PC is 100b0. What are the contents of register a0?**

![Screenshot from 2023-08-19 22-11-33](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/8b7af8b1-5f47-460f-9274-7bf5d6cb34e7)

**6.Debug C program (n=9) with spike and run until PC is 100b0. What are the contents of register sp?**

![Screenshot from 2023-08-19 22-12-14](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/dfcb40fd-3da7-4748-86c7-ce06e9e12fe6)

**7.Debug C program (n=9) with spike and run until PC is 100c4. What are the contents of register a0?**

![Screenshot from 2023-08-19 22-13-19](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/0d489afd-f7a6-446b-ac59-c2f22bc66469)

**8.Debug C program (n=9) with spike and run until PC is 100dc. What is the output on shell?**

![Screenshot from 2023-08-19 22-14-42](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/9f16b60e-137e-4871-a137-182bc66f9360)
 
</details>

## Day-2
<details>
 <summary> Introduction to Application Binary Interface  </summary>
<br>
 The application program can directly access the registers of the RISC V architecture using something known as system calls. The ABI (also known as system call interface enables the application to access the hardware resources via registers.
  
 In RISC V architecture, the width of the register is defined as XLEN. For RV64 and RV32, the widths are 64 bits and 32 bits, respectively.
  
 RISC V belongs to the little endian memory addressing system, which means that the least significant byte of a word is stored in the smallest memory address.

An Application Binary Interface is a set of rules enforced by the operating system on a specific architecture. So, Linker converts relocatable machine code to absolute machine code via ABI interface specific to the architecture of machine.

Just like how application program interface (API) is used by application programs to access the standard libraries, an application binary interface or system  call interface is utilised to access hardware resources . The ISA is inherently divided into two parts: *User & System ISA* and *User ISA*  the latter is available to the user directly by system calls. 
  
Now, how does the ABI access the hardware resources? 
- It uses different registers(32 in number) which are each of width `XLEN = 32 bit` for RV32 (~`XLEN = 64 for RV64`) . On a higher level of abstraction these registers are accessed by their respective ABI names.
  
  For base integer instructions there are broadly 3 types of of such registers:
  - I-type : For instructions having immediate values as operands.
  - R-type : For instructions having only registers as operands.
  - S-type : For instructions used for storing operations.

So, it is system call interface used by the application program to access the registers specific to architecture. Overhere the architecture is RISC-V, so to access 32 registers of RISC-V below is the table which shows the calling convention (ABI name) given to registers for the application programmer to use.

**ABI Block diagram**

![Screenshot from 2023-08-19 12-06-09](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/53b14fd9-f91a-4af3-9934-9460afd3b43b)


</details>
<details>
 <summary> Memory Allocation For Double Words </summary>
<br>
 There are two different ways to load the data into the registers
 1. The 64 bit data can be loaded directly into the registers.
 2.they can be loaded into the registers via memory.
 
 **Example of how memory is allocated for double words**

![Screenshot from 2023-08-19 22-44-16](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/9d8d1747-3437-4324-935a-15d5cec12f90)

![Screenshot from 2023-08-19 22-44-26](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/341eca63-6388-43a7-85ac-808152e093b5)
In the above image the most significant byte sits in top of memory  so it is a **little endian addressing system**
.
![Screenshot from 2023-08-19 12-18-03](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/238899ab-17ed-4aab-9903-33d49ace566a)

![Screenshot from 2023-08-19 12-22-31](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/8d856ddc-bc77-45ca-83e1-b76f80209a3d)
![Screenshot from 2023-08-19 12-22-54](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/367b87b2-441e-4781-9941-6f655e89e7f4)

![Screenshot from 2023-08-19 12-23-41](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/09011b91-4124-4916-bc86-7c823834d200)
 **m[16]-Least significant byte**  **m[23]-most significant byte**
 
</details>

 
<details>

<summary> Load,Add And Store Instructions </summary>

	ld x8,16(x23)
 
 here **ld** is for load doubleword,x8 shows destination register (rd),16 is offset,x23 is source register(rs) . This is I type Instructions  :

<img width="1033" alt="Screenshot 2023-08-19 at 11 24 09 AM" src="https://github.com/alwinshaju08/RISCV/assets/69166205/d9f8e2ce-f424-47dc-934f-b00ef5d9de4a">

	add x8,x29,x8
 
 here **add** is function,x8 is destination register (rd),x29 & x8 is source registers (rs1),(rs2) respectively. This is R type Instructions  :

 ![Screenshot 2023-08-19 at 11 24 19 AM](https://github.com/alwinshaju08/RISCV/assets/69166205/32aeb799-fa17-4dc2-9186-7b142f341f10)

 	sd x8,8(x23)
  
  here **sd** is store doubleword,x8 is data registers(rs2),8 tell offset(immediate) ,x23 is source register(rs1). This is S type Instructions  :

  ![Screenshot 2023-08-19 at 11 31 29 AM](https://github.com/alwinshaju08/RISCV/assets/69166205/b20b0475-88b1-45e1-88cd-84e19cbec61a)

Here in each Instructions set we can see register are of 5 bits so total number of register = 2^5 = 32 registers


**LAB-WORKS**

**1.Modify 1to9_custom.c and load.S as shown in video. What is the output of simulation with -Ofast ?**

![Screenshot from 2023-08-19 23-05-37](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/fc93b7ea-e54d-44c3-b921-9f90c7c73224)

**2.What is the memory location of load subroutine?**

![Screenshot from 2023-08-19 23-06-17](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/7421dc76-d46b-4e56-afb1-4d889053a2f9)

**3.What is the memory location of loop subroutine?**

![Screenshot from 2023-08-19 23-06-51](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/1eb91abf-8f0d-418a-b805-9dd98874c3af)

**4.Open spike debugger and run 1to9_custom.o until PC is 100b0.What is the value of a0 and a1 registers?**

![Screenshot from 2023-08-19 23-08-24](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/0f5f74b8-5240-48a8-90cd-1d83163782bc)

**5.Open spike debugger and run 1to9_custom.o until PC is 100bc.What is the value of a0 and a1 registers?**

![Screenshot from 2023-08-19 23-09-02](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/bf45181a-0ed7-4c50-a342-393d4f341f98)

 </details> 
<details>
 <summary> Lab To Run C-Program On RISC-V CPU </summary>
 
![Screenshot from 2023-08-19 23-16-19](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/5440501b-f84d-4d58-ac0d-d00a25f8ae9c) 
 
Here we have RISCV cpu program code through which we send the HEX format file of c program to show output the output of the given code 

```
chmod 777 rv32im.sh
./rv32im.sh 

```
![Screenshot from 2023-08-19 23-48-34](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/e92eb7e2-2620-475d-826c-a30d8bd039eb)

Input hex file to sent through verilog code:

**firmware.hex:**

![Screenshot from 2023-08-19 23-49-57](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/99f4330d-fb66-4cd7-a37e-8eecaa1aff68)

**firmware32.hex:**

![Screenshot from 2023-08-19 23-51-00](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/7b847007-ace5-4dec-8aab-898b1611800b)

</details>

## Day-3
<details>
 <summary> </summary>
</details>



## Acknowledgement
- Kunal Ghosh, VSD Corp. Pvt. Ltd.
- Skywater Foundry
- Alwin shaju,Colleague,IIIT B
- Emil Jayanth Lal,Colleague,IIIT B
- Pruthvi Parate,Colleague, IIIT B
- Bhargav D V,Colleague, IIIT B


## Reference
- https://www.vsdiat.com
- https://en.wikipedia.org/wiki/Toolchain
- https://en.wikipedia.org/wiki/GNU_toolchain
- https://github.com/riscv/riscv-gnu-toolchain

