
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



**LABWORKS**

**1.What is the value of mabi and march in rv32im.sh script for 1to9_custom.c riscv gcc command?**

![Screenshot from 2023-08-20 10-07-51](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/b327d85a-9e0f-4b38-b717-bd630557e57e)

</details>

## Day-3
<details>
 <summary> Combinational logic in TL-Verilog using Makerchip </summary>
<br>
	
**Introduction to logic gates:**

Logic gates are fundamental building blocks in digital electronics and computer science that perform logical operations on binary signals, which are represented as 0s and 1s. These gates form the foundation of digital circuits, enabling the creation of complex computational systems. Logic gates manipulate binary input signals to produce binary output signals based on specific logical rules.

There are several types of logic gates, each with its own unique behavior. Here is a list of some common types of logic gates:

![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/ea8bdf89-9962-462a-886f-5b59ea624692)</br>

These logic gates serve as the building blocks for creating more complex digital circuits and systems, including arithmetic and memory circuits, processors, and more. They form the foundation of digital computation and are essential in modern technology and electronics.

The basic boolean operators are listed below.

![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/5386590e-01af-48f1-927d-70865af9f794)

**Basic Mux Implementation:**

![Screenshot from 2023-08-20 10-35-51](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/03ec5fce-f27b-4cdb-a4ab-8ca8ba32a18c)</br>

In verilog we  basically use the **ternary operator** to express the functinality of a **Mux**.

```
assign s0? i0:i1; // this  is for a 2x1 Mux

```
**Introduction To Makerchip :**

[Makerchip](https://makerchip.com/) is an online platform that provides an integrated development environment (IDE) for digital design and verification using 
SystemVerilog and TL  Verilog. It allows engineers, students, and enthusiasts to design and simulate digital circuits, develop RTL (Register Transfer Level) 
code, and explore hardware design concepts without requiring the local installation of tools.<br />

To Familiarize oneself with the IDE there are tutorials on the platform where we can experiment.<br />

**TL-Verilog** was used as the HDL of choice for this project. Projects on Makerchip can be completely designed using TL-Verilog. Transaction Level - Verilog standard is an extension of Verilog which has various advantages like simpler syntax, shorter codes and easy pipelining. You can learn more about TL-Verilog [here](http://tl-x.org/).

Timing abstract can be done in TL-Verilog. This model is specified for pipelines where the sequential elements are generated by tools from the pipelined specification. This allows for easy retiming without the risk of introduction of any functional bugs. More information on timing abstract in TL-Verilog can be found in the IEEE paper ["Timing-Abstract Circuit Design in Transaction-Level Verilog" by Steven Hoover](https://ieeexplore.ieee.org/document/8119264).

**Loading Fibonacci Sequence example on Makerchip IDE**

![Screenshot from 2023-08-20 19-32-03](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/9dc3647c-7f12-41c8-a9cb-6d7b5f02004e) 
 
</details>
<details>
<summary> Labs for Combinational logic </summary>
<br>
	
**Lab:Inverter and NAND gates**

![Screenshot from 2023-08-20 21-15-10](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/202cd766-960c-4a41-88d8-7a32d0e524e1)

![Screenshot from 2023-08-20 21-21-48](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/b181258f-d11b-4fdb-a774-884e4ed05007)

**Lab:usage of vectors:**

![Screenshot from 2023-08-20 21-35-48](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/a231e2ef-e0b0-4045-9ecf-c574d8a77237)

**Lab:2X1 Mux**
```
$out = $sel ? $in1 : $in2;
```
![Screenshot from 2023-08-20 21-40-28](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/5da7dac1-2443-40cb-989d-1da43af4544f)

Mux operating on vectors
```
$out[7:0] = $sel ? $in1[7:0] : $in2[7:0];
````
![Screenshot from 2023-08-20 21-44-40](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/fc00367c-68c3-4a24-a02e-558e24a3209d)

**Lab:Combinational Calculator**
```
\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   $reset = *reset;
   
   $val1[31:0] = $rand1[3:0];
   $val2[31:0] = $rand2[3:0];
   
   $sum[31:0] = $val1[31:0] + $val2[31:0];
   $diff[31:0] = $val1[31:0] - $val2[31:0];
   $prod[31:0] = $val1[31:0] * $val2[31:0];
   $quot[31:0] = $val1[31:0] / $val2[31:0];
   
   $out[31:0] = ($op[1:0] == 2'b00) ? $sum[31:0] : ($op[1:0] == 2'b01) ? $diff[31:0] : ($op[1:0] == 2'b10) ? $prod[31:0] : $quot[31:0];
   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule

```
![Screenshot from 2023-08-20 22-18-11](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/2cffa4db-e150-491d-8115-c133cdee9ee4)

	
</details>
<details>
<summary> Sequential logic </summary>
<br>
	
Sequential logic refers to a type of digital logic circuit or system in which the output depends not only on the current inputs but also on the previous states of the circuit. Unlike combinational logic, which only considers the current inputs to generate outputs, sequential logic incorporates memory elements to store information and generate outputs based on both current inputs and past history.

Sequential logic is sequenced by a clock signal.
	
![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/c9f94a6b-9454-4a6a-96d9-d6d452f6069e)

The circuit is constructed to enter a known state in response to a reset signal.

![Screenshot from 2023-08-20 22-27-38](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/29f65790-304d-4c7f-adad-6b323eba32d6)

A D-flip-flop transitions next state to current state on a rising clock edge.

![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/fcc1601b-8fae-43b7-b077-d7a77984a201)

**Lab: Fibonacci sequence**

![WhatsApp Image 2023-08-20 at 22 50 24](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/506709cf-238f-41a6-9db8-021623f6649e)

![WhatsApp Image 2023-08-20 at 22 56 53](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/94c06ff1-002b-4c39-9966-9cf2f5207541)

![Screenshot from 2023-08-20 22-46-55](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/4b4e3328-8e19-48fe-98ad-fcd541b741f7)

**Lab:Counter**

![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/6b626fd7-c24d-4eb1-85d9-f8aa2a515d0d)

![Screenshot from 2023-08-20 23-06-50](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/937a30c2-1013-4e48-9437-06427bf7cf87)

**Lab: Sequential Calculator**

![WhatsApp Image 2023-08-20 at 23 13 46](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/98537f8c-c071-4560-aad0-f744be73e5bd)

![WhatsApp Image 2023-08-20 at 23 19 54](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/20910f30-3b96-4a71-a6a9-585b44324111)

```
\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   $reset = *reset;
   
   $val1[31:0] = $reset ? 0 : >>1$out[31:0] + 0;
   $val2[31:0] = $rand2[3:0];
   
   $sum[31:0] = $val1[31:0] + $val2[31:0];
   $diff[31:0] = $val1[31:0] - $val2[31:0];
   $prod[31:0] = $val1[31:0] * $val2[31:0];
   $quot[31:0] = $val1[31:0] / $val2[31:0];
   
   $out[31:0] = ($op[1:0] == 2'b00) ? $sum[31:0] : ($op[1:0] == 2'b01) ? $diff[31:0] : ($op[1:0] == 2'b10) ? $prod[31:0] : $quot[31:0];
   
   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
![Screenshot from 2023-08-20 23-34-46](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/8b8c40aa-427d-4466-ae47-5bbc637c2b88)

</details>
<details>
<summary> Piplined Logic </summary>	
<br>
Pipelining or timing abstract is an important feature in TL verilog as it can be implemented very easily with fewer codes as compared to system verilog which reduces bugs to a great extent. An example of the pipeling for pythogoras theorem using both TL verilog and system verilog in this repo . In TL verilog pipeling can be implemented by defining the pipeline as |calc and the different pipeline stages should be properly align and are indicated by @1, @2 and so on.	

 Let us glimpse at the Pythagoran's Theorem and compute it in hardware.  
Pythagoran's Theorem: 
Let us compute the pythagoran's theorem over 3 cycles.  
- Cycle1: Squaring on the sides a and b.
- Cycle2: Adding the squared vales of a and b.
- Cycle3: Finding the square root value of the sum.
	
![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/115ebf93-020b-4f9c-8ace-9d306b7c2007)	
 
The timing abstract of the above is: 

![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/ae12c90b-96de-4324-b73e-16b6a9db64a3) 

- **Code reduction** is the most advanatageous property of the TL-Verilog when compared to System Verilog. We can use the above code to compare this:
![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/f3767057-6bbd-49ea-9b27-4cbe96bf3de0)

- The **Retiming** property in TL-Verilog is very easy and safe to implement whereas in SystemVerilog, it is very bug-prone.
  
![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/c12ef629-1b9e-4145-85a9-ffe20c44693e)
![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/6593bb82-2008-46fd-87c3-51605abfc5fd)

- The pipelinig also allows us to run the clock at a high frequency. Regardless of the way we structure our logic, we will be able to produce new set of inputs on every clock edge. As a result, we get high throughput for our circuit.  

![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/985c5034-79de-4db4-9c6c-e3504b8ab806)

The makerchip implementation of  Pythagoran's theorem is given below:

![Screenshot from 2023-08-21 00-16-52](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/dc3f0be7-5270-412b-a693-4dc9b23c8792)
Identifiers and Types
![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/515486d0-ffea-4a76-92c9-19f7a37c1620)

**Fibonacci series in a pipeline**

![WhatsApp Image 2023-08-21 at 00 33 42](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/2e8e24e9-fb50-47e8-acc7-5cfc50676005)

**Lab:Pipeline**

![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/4c8a1efd-0ce1-43e8-aea6-21b38aad8448)

![Screenshot from 2023-08-21 01-04-13](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/e395226f-d042-4468-adaf-20148ac33873)

**Lab:Counter and Calculator in pipeline**

![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/1ee6edfb-d4eb-419c-8e4f-aba42e296a79)

```
\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   
   |calc
      @1
         $reset = *reset;
   
   
         $cnt = $reset ? 0 : >>1$cnt + 1'b1;
         $val1[31:0] = $reset ? 0 : >>1$out[31:0] + 1'b0;
         $val2[31:0] = $rand2[3:0];
   
         $sum[31:0] = $val1[31:0] + $val2[31:0];
         $diff[31:0] = $val1[31:0] - $val2[31:0];
         $prod[31:0] = $val1[31:0] * $val2[31:0];
         $quot[31:0] = $val1[31:0] / $val2[31:0];
   
         $out[31:0] = ($op[1:0] == 2'b00) ? $sum[31:0] : ($op[1:0] == 2'b01) ? $diff[31:0] : ($op[1:0] == 2'b10) ? $prod[31:0] : $quot[31:0];
   
   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```

![Screenshot from 2023-08-21 01-19-58](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/e49a9f93-4b71-4be6-96e2-28e81590fcc7)

**Lab: 2-Cycle calculator**

![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/3d77e7b3-cde8-4a89-836b-51328afff0af)

```
\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   
   |calc
      @1
         $reset = *reset;
   
   
         $valid = $reset ? 0 : >>1$valid + 1'b1;
         $val1[31:0] = >>2$out[31:0];
         $val2[31:0] = $rand2[3:0];
   
         $sum[31:0] = $val1[31:0] + $val2[31:0];
         $diff[31:0] = $val1[31:0] - $val2[31:0];
         $prod[31:0] = $val1[31:0] * $val2[31:0];
         $quot[31:0] = $val1[31:0] / $val2[31:0];
      @2
                
         $out[31:0] = ($reset + ! $valid) ? 32'b0:(($op[1:0] == 2'b00) ? $sum[31:0] : ($op[1:0] == 2'b01) ? $diff[31:0] : ($op[1:0] == 2'b10) ? $prod[31:0] : $quot[31:0]);
   
   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
![Screenshot from 2023-08-21 16-51-22](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/0f7dafc1-d178-4f77-b357-01502e897315)

</details>

<details>
<summary> Validity </summary>	
<br>
	
**Validity** is another feature in TL verilog which is asserted if a particular transactions in a pipeline is valid or true. A new scope, called “when” scope is introduced for this and it is denoted as **?$valid**. This new scope has many advantages - easier design, cleaner debug, better error checking and automated clock gating.
<br>	
	
Validity provides :
1. Easier debug
2. Cleaner design
3. Better error checking
4. Automated Clock gating
</br>

**Clock gating:**
<br>

Clock gating is a technique used in digital circuit design to save power by selectively controlling the clock signal to different parts of a circuit. In digital systems, the clock signal is used to synchronize the operations of various components within the circuit. However, not all parts of a circuit need to be active and consuming power all the time. Clock gating helps reduce power consumption by disabling the clock signal to certain circuit elements when they are not needed.

The basic idea behind clock gating is to insert logic gates (typically AND or OR gates) between the clock source and the destination registers or logic elements. These gates act as switches that allow the clock signal to pass through only when a certain condition is met. If the condition is not satisfied, the clock signal is effectively "gated" or blocked from reaching the destination, preventing unnecessary clock cycles and power consumption.

Clock gating can be implemented at various levels of a design, ranging from individual registers to larger functional blocks or subsystems. It is particularly effective in designs where certain parts of the circuit are idle for significant periods of time.

Benefits of clock gating include:

1. **Power Savings**: By preventing clock signals from reaching inactive components, clock gating reduces dynamic power consumption, which is the power consumed when transistors switch states.

2. **Heat Reduction**: Lower power consumption leads to reduced heat generation, which is especially important in modern high-performance and mobile devices where heat dissipation is a concern.

3. **Extended Battery Life**: In battery-powered devices, clock gating contributes to longer battery life by conserving power.

4. **Improved Performance**: In some cases, clock gating can also help improve performance by allowing certain parts of the circuit to operate at higher frequencies since overall power consumption is reduced.

However, clock gating isn't always straightforward. If implemented incorrectly, it can introduce additional delay into the circuit, impacting performance. Additionally, managing clock domains and ensuring proper synchronization between clock-gated and non-clock-gated regions can be complex.

In summary, clock gating is a power-saving technique in digital design that selectively disables clock signals to inactive parts of a circuit, leading to reduced power consumption and associated benefits.

- Clock gating avoids toggling clock signals.
- TL-Verilog can produce fine-grained gating (or enables).

**Lab: Distance accumulator**
```
\m4_TLV_version 1d: tl-x.org
\SV
   `include "sqrt32.v";
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   |calc
      @1
         $reset = *reset;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] * $aa;
            $bb_sq[31:0] = $bb[3:0] * $bb;
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
      
      @4
         $tot_dist[63:0] = 
             $reset ? '0 :
             $valid ? >>1$tot_dist + $cc :
                      >>1$tot_dist;
     
         
!  *passed = *cyc_cnt > 16'd30;        
   
  
   
   
\SV
   endmodule
```
![Screenshot from 2023-08-21 18-00-15](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/3b8d2592-079e-4363-bc1e-f6a38cd3e45b)</br>

**Lab: 2-Cycle Calculator with Validity**

```
\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   |calc
      @1
         $reset = *reset;
         $valid = $reset ? 0 : >>1$valid + 1'b1;
         $valid_or_reset = $valid || $reset;
      ?$valid_or_reset   
         @1
            $val1[31:0] = >>2$out[31:0];
            $val2[31:0] = $rand2[3:0];



            $sum[31:0] = $val1[31:0] + $val2[31:0];
            $diff[31:0] = $val1[31:0] - $val2[31:0];
            $prod[31:0] = $val1[31:0] * $val2[31:0];
            $quot[31:0] = $val1[31:0] / $val2[31:0];

         @2
            $out[31:0] = $reset ? 32'b0 : (($op[1:0] == 2'b00) ? $sum[31:0] : ($op[1:0] == 2'b01) ? $diff[31:0] : ($op[1:0] == 2'b10) ? $prod[31:0] : $quot[31:0]);


   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
endmodule
```
![Screenshot from 2023-08-21 18-49-32](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/132e185b-4762-4098-8f5e-10a4cb13fa4c)</br>

**Lab: Calculator with Single value memory**

```
\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   |calc
      @1
         $reset = *reset;
         $valid = $reset ? 0 : >>1$valid + 1'b1;
         $valid_or_reset = $valid || $reset;
      ?$valid_or_reset   
         @1
            $val1[31:0] = >>2$out[31:0];
            $val2[31:0] = $rand2[3:0];



            $sum[31:0] = $val1[31:0] + $val2[31:0];
            $diff[31:0] = $val1[31:0] - $val2[31:0];
            $prod[31:0] = $val1[31:0] * $val2[31:0];
            $quot[31:0] = $val1[31:0] / $val2[31:0];

         @2
            $out[31:0] = $reset ? 32'b0 : (($op[2:0] == 3'b000) ? $sum[31:0] : ($op[2:0] == 3'b001) ? $diff[31:0] : ($op[2:0] == 3'b010) ? $prod[31:0] : ($op[2:0] == 3'b011) ? $quot[31:0] : ($op[2:0] == 3'b100) ? $recall : >>2$out);
            $recall[31:0] = >>2$mem[31:0];
            $mem[31:0] = $reset ? 32'b0 : (($op[2:0] == 3'b101) ? >>2$out : '0);

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
\SV
endmodule
```
![Screenshot from 2023-08-21 20-09-23](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/9e321784-312a-44cc-ae9f-9f274d3584b0)

</details>

<details>
<summary> Wrap-up </summary>	
<br>	
	
**Lab: pythagarous theroem using hierarchy**

![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/28cdb06f-a55b-458d-accb-7350f655db2a)
```
\m4_TLV_version 1d: tl-x.org
\SV
   `include "sqrt32.v";
   m4_makerchip_module
\TLV

   |calc
      
      // DUT
      /coord[1:0]
         @1
            $sq[9:0] = $value[3:0] ** 2;
      @2
         $cc_sq[10:0] = /coord[0]$sq + /coord[1]$sq;
      @3
         $cc[4:0] = sqrt($cc_sq);


      // Print
      @3
         \SV_plus
            always_ff @(posedge clk) begin
               \$display("sqrt((\%2d ^ 2) + (\%2d ^ 2)) = %2d", /coord[0]$value, /coord[1]$value, $cc);
            end

\SV
endmodule
```
![Screenshot from 2023-08-21 20-49-18](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/7477d529-101e-48a2-8632-83efef431b4e)

</details>

## Day-4

<details> 
<summary> Introduction to simple RISC-V Micro architecture </summary>
<br>
The block diagram of a basic RISC-V microarchitecture is as shown in figure below. Now, using the Makerchip platform the implementation of the RISC-V microarchitecture or core is done. For starting the implementation a starter code present [here](https://github.com/stevehoover/RISC-V_MYTH_Workshop) is used. The starter code consist of -

- A simple RISC-V assembler.
- An instruction memory containing the sum 1..9 test program.
- Commented code for register file and memory.
- Visualization.

  **RISC-V Block Diagram**
  
  ![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/ae01f90c-3cbe-4210-8f67-05f81cec06c9)

  Here's a brief explanation of each component:

    **Instruction Memory**: This is where the CPU fetches instructions from memory. The program counter (PC) points to the address of the next instruction to be fetched.

    **Instruction Fetch/Decode**: In this stage, fetched instructions are decoded to identify their type and operands.

    **Register File**: This is a set of registers where data is temporarily stored. Instructions can read from and write to these registers.

    **ALU/Execution**: The Arithmetic Logic Unit (ALU) performs arithmetic and logical operations on data from the register file. This stage also includes execution units for other types of    instructions, like memory access and branching.

    **Data Memory**: This is where data is read from or written to memory. It interacts with the ALU and the register file.

    **Writeback/Commit**: After executing an instruction, the result is written back to the register file if necessary. This stage also handles updating the program counter based on the outcome of branching instructions
  
  **Program Counter**: (PC) also known as the Instruction Pointer (IP) in some architectures, is a fundamental component in the design of a computer's central processing unit (CPU). It plays a crucial role in the execution of instructions and the control flow of a program. The Program Counter keeps track of the memory address of the next instruction to be fetched and executed.


</details>

<details>
<summary> Fetch and Decode </summary>	
<br>
Designing of processor is based on three core steps fetch, decode and execute :

Here we gonna design RISC-V Cpu Core for which block diagram is given below :


![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/ba691dab-0cdc-40bb-a0e5-bb30e717090b)


## Template For Running Viz:

```
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;



      // YOUR CODE HERE
      // ...

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      //m4+imem(@1)    // Args: (read stage)
      //m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
      //m4+myth_fpga(@0)  // Uncomment to run on fpga

   //m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
   endmodule
```
## Lab-1 : PC Logic

The program counter (PC) is a fundamental component of a computer's central processing unit (CPU) that keeps track of the address of the next instruction to be fetched and executed. The PC logic manages the updating of the program counter as instructions are fetched and executed in a program.

**Incrementing the PC:**
After an instruction is fetched, the PC needs to be updated to point to the next instruction's address. The most common approach is to increment the PC by the size of the instruction. In many architectures, instructions are of a fixed size, such as 32 bits, so the PC is incremented by 4 after each instruction fetch.

![Screenshot from 2023-08-22 11-30-33](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/05e146ca-7698-42e1-a1c4-45f2f54b96b1)

```
|cpu
      @0
         $reset = *reset;
         
         $pc[31:0] = >>1$reset ? '0 : >>1$pc + 32'd4;
```

![Screenshot from 2023-08-22 11-44-25](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/ad91d393-13ae-41f0-9a4b-7aa645b898de)

## Lab-2 : Instruction Fetch Logic

![Screenshot from 2023-08-22 11-56-31](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/53839638-0fff-46c5-a4a3-5721f74c1322)

```
|cpu
      @0
         $reset = *reset;
         
         $pc[31:0] = >>1$reset ? '0 : >>1$pc + 32'd4; 

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      //m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
      //m4+myth_fpga(@0)  // Uncomment to run on fpga

   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
   endmodule
```

![Screenshot from 2023-08-22 12-01-27](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/06a306b9-2d78-4727-bcda-c909e930f396)

In the log we will observe a warning
```
WARNING(1) (UNUSED-SIG): File 'top.tlv' Line 61 (char 16)
			-> instantiated: '/raw.githubusercontent.com/BalaDhinesh/RISCVMYTHWorkshop/master/tlvlib/riscvshelllib.tlv':32, which
	resulted in 'top.m4':74(ch16):
	+---------------vvvvvvvvvvvvvvvvvvv-------
	>               $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
	+---------------^^^^^^^^^^^^^^^^^^^-------
	Signal |cpu$imem_rd_data is assigned but never used.
```
![Screenshot from 2023-08-22 12-08-37](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/3f2d842c-4977-4da8-849d-0b6a32d3ce97)

```
|cpu
      @0
         $reset = *reset;
         //pc
         $pc[31:0] = >>1$reset ? 32'b0 : >>1$pc + 32'd4;
      @1   
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;   
         $instr[31:0] = $imem_rd_data[31:0];
         
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;   

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      //m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
      //m4+myth_fpga(@0)  // Uncomment to run on fpga

   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
  endmodule
```
![Screenshot from 2023-08-22 12-40-46](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/9770d4f1-327d-41c8-ba6c-7349ca34bbb0)

![Screenshot from 2023-08-22 12-45-08](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/7db28fe6-a04f-4de8-b11a-097a558d027d)

## Lab-3: RISC-V Instruction Types IRSBJU Decode Logic

In computer architecture, instruction decoding is the process of interpreting the bits of an instruction fetched from memory to determine the operation that the instruction is supposed to perform. Different instruction types have distinct formats and meanings, and the decoding process varies accordingly. Below, I'll provide a general overview of common instruction types and their decoding:

1. **R-Type (Register-Type) Instructions:**
   R-Type instructions operate on data stored in registers. They usually involve arithmetic, logical, or shift operations.
   
   Format: 
   ```
   opcode | rd | funct3 | rs1 | rs2 | funct7
   ```
   
   - `opcode`: Operation code.
   - `rd`: Destination register.
   - `funct3`: Function code specifying the operation.
   - `rs1`: Source register 1.
   - `rs2`: Source register 2.
   - `funct7`: Additional function code (used for certain instructions).

2. **I-Type (Immediate-Type) Instructions:**
   I-Type instructions perform operations with an immediate value (constant) and a register.
   
   Format:
   ```
   opcode | rd | funct3 | rs1 | imm[11:0]
   ```
   
   - `opcode`: Operation code.
   - `rd`: Destination register.
   - `funct3`: Function code specifying the operation.
   - `rs1`: Source register.
   - `imm[11:0]`: 12-bit immediate value.

3. **S-Type (Store-Type) Instructions:**
   S-Type instructions store data from a register into memory.
   
   Format:
   ```
   opcode | imm[11:5] | rs2 | rs1 | funct3 | imm[4:0]
   ```
   
   - `opcode`: Operation code.
   - `imm[11:5]`: Upper immediate bits.
   - `rs2`: Source register 2.
   - `rs1`: Source register 1.
   - `funct3`: Function code specifying the operation.
   - `imm[4:0]`: Lower immediate bits.

4. **B-Type (Branch-Type) Instructions:**
   B-Type instructions perform conditional branches based on comparisons.
   
   Format:
   ```
   opcode | imm[12] | imm[10:5] | rs2 | rs1 | funct3 | imm[4:1] | imm[11] | imm[0]
   ```
   
   - `opcode`: Operation code.
   - `imm[12]`: Upper immediate bit.
   - `imm[10:5]`: Immediate bits for offset calculation.
   - `rs2`: Source register 2.
   - `rs1`: Source register 1.
   - `funct3`: Function code specifying the operation.
   - `imm[4:1]`: Immediate bits for offset calculation.
   - `imm[11]`: Immediate bit.
   - `imm[0]`: Immediate bit.

5. **U-Type (Upper Immediate-Type) Instructions:**
   U-Type instructions load a constant into a register.
   
   Format:
   ```
   opcode | rd | imm[31:12]
   ```
   
   - `opcode`: Operation code.
   - `rd`: Destination register.
   - `imm[31:12]`: 20-bit immediate value.

6. **J-Type (Jump-Type) Instructions:**
   J-Type instructions perform unconditional jumps.
   
   Format:
   ```
   opcode | rd | imm[20] | imm[10:1] | imm[11] | imm[19:12]
   ```
   
   - `opcode`: Operation code.
   - `rd`: Destination register.
   - `imm[20]`: Immediate bit.
   - `imm[10:1]`: Immediate bits for offset calculation.
   - `imm[11]`: Immediate bit.
   - `imm[19:12]`: Immediate bits for offset calculation.

These are the main instruction types in many RISC architectures, including RISC-V. When an instruction is fetched from memory, the instruction decoder uses the opcode and other fields to identify the instruction type and the operands involved. Based on the instruction type, the CPU can then execute the appropriate operation using the decoded values. Keep in mind that this is a high-level overview, and the specifics might vary based on the architecture and implementation details.

![image](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/16968e0d-9de9-47fa-b3f3-13c68a057cfc)

![Screenshot from 2023-08-22 12-58-36](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/467b035c-92ec-42ce-8362-fa16369d5164)

```
|cpu
      @0
         $reset = *reset;
      @1
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==? 5'b11001 ;
                       
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==? 5'b10100 ; 
                       
         $is_s_instr = $instr[6:2] ==? 5'b0100x ;
         
         $is_u_instr = $instr[6:2] ==? 5'b0x101 ;
         
         $is_b_instr = $instr[6:2] ==? 5'b11000 ;
         
         $is_j_instr = $instr[6:2] ==? 5'b11011 ;
                                     
      // YOUR CODE HERE
      // ...

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      //m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
      //m4+myth_fpga(@0)  // Uncomment to run on fpga

   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
   endmodule
```
![Screenshot from 2023-08-22 13-18-54](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/297451c1-d1c0-42fb-b5dc-d8f8ea256393)

![Screenshot from 2023-08-22 12-45-08](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/6e032dda-c9d4-492e-8a78-bf33bb672c27)

## Lab-4: Instruction Immediate Decode Logic For RV-ISBUJ 

![Screenshot from 2023-08-22 18-38-53](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/67924b5f-c273-4255-9c38-423d0811634f)

```
//immediate instr
         $imm[31:0] = $is_i_instr ? { {21{$instr[31]}}, $instr[30:20] } :
                      $is_s_instr ? { {21{$instr[31]}}, $instr[30:25], $instr[11:8], $instr[7] } :
                      $is_b_instr ? { {19{$instr[31]}}, {2{$instr[7]}}, $instr[30:25], $instr[11:8], 0 } :
                      $is_u_instr ? { $instr[31], $instr[30:20], $instr[19:12], 0 } :
                         $is_j_instr ? { {21{$instr[31]}}, $instr[19:12], {2{$instr[20]}}, $instr[30:25], $instr[24:21], 0 } :
                         32'b0;
```

![Screenshot from 2023-08-22 19-13-43](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/683d2f5c-e686-42ab-ad05-68a2fe1cd31c)

![Screenshot from 2023-08-22 12-45-08](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/cfcaa06f-93b0-4704-a153-f5c316c8bd53)

## Lab-5: Decode other Fields of Instructions For RV-ISBUJ 

![Screenshot from 2023-08-22 19-19-50](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/08278573-23fd-44b1-8cb3-0d555981efb0)

```
//extracting other instruction fields
         $rs2 = $instr[24:20];
         $rs1 = $instr[19:15];
         $rd = $instr[11:7];
         $opcode = $instr[6:0];
         $funct3 = $instr[12:14];
         $funct7 = $instr[25:30];

```
![Screenshot from 2023-08-22 19-29-01](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/57d793f4-eeba-4813-84af-9b4bd79161f2)

![Screenshot from 2023-08-22 19-31-24](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/cab61f80-fb61-4970-abdb-1952d9981b27)

## Lab-6: To Decode Instruction Field Based on Instr Type RV-ISBUJ 

![Screenshot from 2023-08-22 19-33-38](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/22b83cc7-bc9e-4ac7-944a-29a79e4fbd06)

```
//instruction field code
         
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         $rs1_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         $funct3_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         $funct7_valid = $is_r_instr; 
         ?$funct7_valid
            $funct7[5:0] = $instr[25:31];
         $opcode_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr || $is_s_instr || $is_b_instr;
         ?$opcode_valid
            $opcode[4:0] = $instr[11:7];


```

![Screenshot from 2023-08-22 19-52-35](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/21471a83-b240-4164-a8be-743905f1ebca)

![Screenshot from 2023-08-22 19-53-29](https://github.com/NSampathIIITB/Introduction-to-RISC-V-Architecture/assets/141038460/862bf92a-10c7-4d69-9cce-dd455abbaaab)










  
</details>





## Day-5






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

