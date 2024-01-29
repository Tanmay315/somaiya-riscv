# RISCV

- [DAY1: Introduction to RISCV ISA and GNU compiler toolchain](#DAY1--Introduction-to-RISCV-ISA-and-GNU-compiler-toolchain)
  
- [DAY2: Introduction to ABI and basic verification flow](#DAY2--Introduction-to-ABI-and-basic-verification-flow)

# DAY1: Introduction to RISCV ISA and GNU Compiler Toolchain
<details>
  <summary>Installation</summary>
  1. Ensure that your device has at least 100GB of free space on any drive.

2. Download the vsdsquadron VDI from the following link: [vsdsquadron.vdi](https://forgefunder.com/~kunal/vsdsquadron.vdi).

3. Download VirtualBox from the official website: [VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads).

4. Create a new virtual machine:
   - Type: LINUX
   - Version: Ubuntu 18.04 (64-bit)
   - Memory: 4096MB for base memory
   - Processors: 4

5. Create a virtual hard disk:
   - Choose "Use an existing virtual hard disk file."
   - Click on the folder icon to browse to the location of the downloaded VDI file on your Windows computer.

6. Finish the setup process.

7. Start the virtual machine by clicking on the start arrow.
<img width="682" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202023-12-30%20122419.png">
</details>
<details>
  <summary>
     Introduction to RISCV basic keywords
  </summary>


 Introduction 

  
In introduction we will see course overview of our course i.e.

Firstly, a C/C++/Java program can be converted to an assembly language in riscv architecture and then it is converted to a bit stems of zeros and once which is then given to the hardware to process the given program which can be seen in the image given below. 

<img width="682" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20110512.png">

From apps to hardware:



As we have seen in the above section that how an C program is converted to assembly language and given to the hardware, now we will see this same thing with an example of an application software.

<img width="682" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20111124.png">

 Description of course contents:

In this course we will see the whole riscv architecture and all the instructions which are included in this architecture.
1. Pseudo Instructions
2. Base  integer instructions(RV4I)
3. Multiply extension(RV64M)
4. Single and double precision floating point extension(RV64F and RV64D)
5. Application binary interface(ABI)
6. Memory allocation and stack pointer.



</details>

<details>
  <summary>
    Software Toolchain
  </summary>

  C program to compute sum from 1 to n:

```
#include <stdio.h>
int main()
{
int n=5, y=0, i;

for (i=0; i<=n; i++)
{
  y = y + i;
}
printf("Required sum is: ", y);
return 0;
}

```

On executing the above program we get our desired output.
<img width="682" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20113314.png">



In the above case we have compiled the program using Windows compiler, now we will compile the above program using riscv compiler and see what we get as a result.To get the result of riscv compiler we will use the following instructions in the same order as given below in the terminal. 

1. riscv64-unknown-elf-gcc -o1 mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
2. ls -ltr sum1ton.o
3. riscv64-unknown-elf-objdump -d sum1ton.o
4. riscv64-unknown-elf-objdump -d sum1ton.o | less
5. /main
6. Press n

<img width="682" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20122247.png">


If we were try to figure out number of instructions, it turns out to be

(101b0 - 10184) / 4 = 15 instructions

For compilation of the program use the following command
```
     riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```
To view the output use spike simulator as follows
```
spike pk <filename.o>
```
After compilation we get
<img width="682" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/296809297-575e2af3-1589-4a36-b5f0-8703b5defdc7.png">

For debugging use the following command
```
spike -d pk <filename.o>
```


</details>

<details>
  <summary>Integer number representation
</summary>

  64-bit Number System for Unsigned Numbers

While converting the Assembly language instructions to bid streams of zeros and ones if we encounter a human understandable number like a decimal value so it is also converted to 0/1 bit stream.

8 bit = Byte
4 Bytes = Word
2 Word or 8 Byte = Double word

Total Number of patterns that can be represented:
For 2 bit:
Total Patterns = 2*2
For 3 bit:
Total Patterns = 2*2*2

Following is the way to convert bit stream to decimal value:

<img width="682" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20125647.png"> 


Following are some important points to be remembered:

<img width="682" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20125826.png"> 

64-bit Number System for Signed Numbers:

When we have a negative number in signed numbers of 64 bit number system so for that we will use two's complement method to get the corresponding bitstream of zeros and ones.

To find the negative number: We do so through 2's complement method
- Find binary equivalent of given number
- Find 1's complement(invert individual bits)
- Then we add 1 to the LSB of the bit sequence to get result

<img width="482" src="https://th.bing.com/th?id=OIP.Tl9nfwRGllFo28mQzoYdGQAAAA&w=299&h=157&c=8&rs=1&qlt=90&o=6&pid=3.1&rm=2">  

Here are some important points that we need to remember before moving towards the labs,

<img src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20130614.png" width="682">

Lab for Signed and Unsigned Numbers:

Code to find the highest unsigned number in 64 bit:

```
#include<stdio.h>
#include<math.h>
int main(){
unsigned long long int max=(unsigned long long int)(pow(2,64)-1);
 printf(“Highest number represented by unsigned long long int is %llu\n”,max);
return 0;
}
```

Following is the output of the above program:

<img src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20132101.png" width="682">

</details>

# DAY2: Introduction to ABI and basic verification flow
<details>
  <summary>Application Binary Interface
</summary>


Introduction to ABI:

- ABI is an interface through which users can directly access the registers of the 
  riscv architecture registors through system golf.
- In Riscv architecture we have a total 32 registers.
- The weight of the register is defined by XLEN i.e.
  For RV32, XLEN is 32 bit
  For RV64, XLEN is 64 bit

Memory allocations for Double words:

Let's take XLEN as 64 bit as for RV64

<img width="682" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20150724.png"> 

- RISCV belongs to “Little-endian” memory addressing system.
- Address of first double word is m[0]
Address of second double word is m[8]
Address of third double word is m[16]

Load,add and Store instructions with examples:

<img width="682" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20152647.png"> 

- All the instructions in 64 bit or 32 bit RV are 32 bit that is all the instructions will have only 32 bit space.
- Command to load a double word stored at 16 to 23 memory location to x8 register is, ld x8,16(x23);
here ‘ld’ is load double word, ‘x8’ is destination register rd, 16 is the offset ‘imm’ and ‘x23’ is the source register rs1.


<img src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20153156.png" width="682"> 

 - Command to add the contents of two register and store it  to a third register is given as, add x8,x24,x8;
 where add is the addition of double word, x8 is the destination register rd, x24 is the source register rs 1 and x8 is the source register rs2.
<img src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20153622.png" width="682"> 


- Command to store the data of one register to another register is given as, sd x8, (x23);
Where sd is store doubleword, x8 is data register rs2,8 is offset ‘imm’ and x23 is the source register rs1.


<img src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20154001.png" width="682"> 

- Here in the above example load instruction is the ‘I type’ instruction, add instruction is the ‘R type’ instruction and Store instruction is the ‘S type’ instruction.
- All the registers present in the different instructions like rs1, rd, rs2 have only 5 bits to represent, so total number of registers equals to 2 to the power 5 which is nothing but 32 registers that that's why we have only 32 registers in riscv architecture.


<img src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-03%20154600.png" width="682"> 

</details>

<details>
  <summary>Study new Algorithm for sum 1 to N using ASM</summary>

  Algorithm for C program of finding sum of 1 to N numbers using ASM woul be;

  <img width="684" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-04%20133809.png">
</details>

<details>
  <summary>Review ASM Function call</summary>
  
  Modified code for finding the Sum of 1 to 9 is as follows:

  ```
  #include <stdio.h>

  extern int load(int x, int y)

  int main(){
              int result = 0;
              int count = 9;
              result = load(0x0, count+1);
              printf("Sum of numbers 0 to %d is %d ", count, result);
  }
  ```

<img width="684" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-04%20142103.png">
</details>

<details>
  <summary>Lab to run C program on RISC V CPU</summary>
  
   - Here we will run the C program on RISC V CPU which is written in verilog.

  
  - For it we will convert the C program to a Hex format file and store it in memory.


 - Then that Hex format file is given to RISC V CPU.


 - And the CPU will display the sum of numbers from 1 to N.

  <img width="684" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-04%20155303.png">

  <img width="684" src="https://github.com/Tanmay315/somaiya-riscv/blob/main/Screenshot%202024-01-04%20155745.png">
</details>


