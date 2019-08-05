# Boolean Logic
All digital devices are made from elementary logic gates.

## Background
Talks about Boolean Algebra, Boolean Functions and its implementation using Boolean gates.

### Boolean Algebra
Boolean (binary) values are labeled as true/false, on/off, yes/no, etc we use 1 and 0. Boolean function operates on boolean values and produces boolean output. Since computers primarily operate by manipulating binary values, *boolean functions* play a central part of hardware architecture.

In HTDP, we do write function examples by listing some input values and expected output values. Like that if we list all possible binary input values and its output, it is called *Truth Table Representation*

In addition to truth table, we also specify boolean operations that done by a boolean functions. Those operations are called boolean expression and typically uses `AND`, `OR` and `Not` operations

For example, 
1. `f(x, y z)` is boolean function
2. (x + y) . ž
3. Truth table 
![image](images/truth-table-1.png)

**Canonical Representation** Boolean functions can be representated by only using boolean expressions, `and, or and not`

From the truth table, let us take only rows that result in 1.
3rd row can be represented as (Not(x) AND y AND Not(z))

Similarly 5th row is
(x AND Not(y) AND Not(z))
7th row is (x AND y AND Not(z))

Interestingly, we can use NAND gate to construct AND, OR and Not gates. So basically, using one NAND gate implementation we can build a computer

### Gate Logic
A gate is a physical device that implements a boolean function. A electrical (electronics in india) engineer implements basic gates using transistors. A hardware engineer uses them and connects them in variety of ways to create more sophisticated and complex gates.

A gate has been represented by two pharases. Gate interface and gate implementation. Gate interface tells about the boolean function we need and stated mostly in terms of truth table.

A Gate implementation achieves the truth tables by connecting various basic gates. Note that there is multiple ways of achieving this. The rule of thumb is that we should use as much less gates as possible to implement a interface for efficiency.

### Actual Hardware Construction
We can assemble logic gates using transistors, soldering rod, lead, circuit board, etc. But it is difficult to built a physical gate and then test it to make sure it works correctly. So we found an alternative, easy way to design hardwares

### Hardware Description Language
We use HDL and hardware simulation software to design complex gates. By this way, we don't have to physically produce any gates, but use programming and software to produce diagram of desired gate, test it and bench mark its efficiency. If all is well, then we can proceed to produce it physically

### Hardware Simulation
After writing code in HDL we use hardware simulation software to compile and test the code.

## Specification
Specifications of basic gates such as NAND, Not, AND, OR, XOR, Multiplexor and Demultiplexor and Multi bit version of gates

https://www.electronics-tutorials.ws/combination/comb_2.html

# Boolean Arithmetic
Adding numbers is a basic operation and is base for other operations such as multiplication.

## Background
Explains about binary number system. Converting decimal to binary and vice versa. Also explained about *signed* numbers. How 2's compliment is used to represent signed numbers. 2's complement can be calculated by fliping each bit in sequence of bits and then add 1 to it. For example, 5 is represented in binary as `0101`. By flipping bits, it becomes `1010` and by adding one to it, it becomes `1011` which is represented as `-5`

## Specification
Gives specifications for chips

### Adders
- HalfAdder 
- FullAdder
- Add16 => Adder (16 Bit)
- Inc16 => Increment by One

### The Arithmetic Logic Unit (ALU)
Authors carefully designed a simple, elegant and efficient ALU specification which uses two 16bit inputs and one 16bit output and two info bits. Which operation should taken care of by ALU is controlled by six control bits such as
**Input**
- x => 16 bit input
- y => 16 bit input
- zx => changes input x to zero (if zx == 1)
- nx => negates input x (if nx == 1)
- zy => changes input y to zero (if zy == 1)
- ny => negates input y (if ny == 1)
- f => function to execute. if f == 1 then out=x+y else out=x&y
- no => negates the output
**Output**
- out => 16 bit output
- zr => zr is 1, if out == 0
- ng => ng is 1, if out < 0

## Implementation
Gives tip and info for implementing above mentioned chips

## Perspective
Designing an ALU is a trade off. If operations such as multiplication and division are implemnted in hardware, then the cost of hardware become expensive, but is highly efficient and fast.

On the other hand, by implementing a simple ALU such as authors suggest, will result in less expensive chip. Other operations can be taken care by operating system software which will slow down the arithmetics.

# Sequential Logic
So far we have seen chips such as NAND and ALU that can compute values based on given inputs. However, they can't maintain state. If suppose, we need to add 3 numbers, They can't remember sum of 2 numbers which will be used to add with 3rd number.

The most basic gate that can remember and maintain state is called Flip Flop.

## Background
**The Clock** Most computers has a clock chip that produces continuous train of alternating signal. i.e 0 and 1 or tick and tock. Both 0 and 1 (or tick and tock) is called one cycle. 

**Flip Flops** A data flip flop is a basic chip that outputs a previous input.
i.e. `out[t] = in[t-1]`. In other words, let us say the input changes continually based on `clock cycle`, the output of this chip is the input which is happen to be one cycle before current one.

**Registers** A register is a storage device that can `store` a value for desired amount of clock cycles.
![image](images/1-bit-register.png)

**w-bit Register** `w` stands for word. If we built 16 bit computer, then word size is 16 bits. We can also built 32 and 64. This can be done by combining 1 bit registers
![image](images/w-bit-register.png)

**Memory Banks** Once we have w-bit registers, we can built arbitrary length of memory banks by combining registers
![image](images/memory-banks.png)

**Counters** A counter increments an integer number for every clock cycle. Typically, a **Program counter** holds memory address of currently executing instruction. As the time passes, a cycle completed, the `PC` increments its content (i.e. next address) which happen to be location of next instruction

## Specification
Specification given for the following chips by authors
- Data Flip Flop
- Registers
- Memory
- Counter

## Implementation

### Data Flip Flop
This chip is given to us just like NAND chip. We don't need to implement this

### 1 Bit Registers
This can be implemented using Mux, DFF

### w-Bit Registers
This can be implemented by arraying up 1 Bit Registers

### Memory Banks
Once we have w-Bit Registers, we can built any arbitrary length of Memory banks using Mux, array of w-Bit Registers and DMux

### Counters
This can be implmented in the same way ALU is implemented.

# Machine Language
So far we developed basic gates and ALU. ALU is capable of doing arithmatic and logic operations for given binary input. And we built sequential logic gates which is capable of remembering state. Generally, computers store a set of binary inputs (a.k.a machine language program) using sequantial logics gates and execute the program instruction by instruction using Program Counter.

So it is necessary to understand what a machine language is, how to program using it and how our hardware interprets and reacts to it. Only then we can be able to built a complete computer.

## Background
To understand machine language in isolation, we can abstract hardware platform and only use three main abstractions such as a processor, memory and registers

### Machines
A machine language can be viewed as an agreed-upon formalism, designed to manipulate a memory using a processor and a set of registers.

### Languages
In a 16bit computer, a typical instruction will look like this `1010001100011001` which may consist of four 4bit information such as operation, and operands. For example, it may read as ADD, R1, R2, R3
This instruction adds content of R1 (RAM register 1) and R2 and then store it in R3. In certain context, it well may mean a 16 bit memory address.

The symbolic representation (ADD) is called `MNEMONICS`. Since it is difficult to write programs using 0s and 1s, we use symbolic representation and then a software called `assembler` will translate this symbolic code into binary instructions.

### Commands
There are few types of commands
**Arthimetic and logic operations** As we saw earlier, it goes like this
```
ADD R2,R1,R3 // R2 <- R1+R3 where R1, R2 and R3 are registers
AND R1,R1,R2 // R1 <- bit wise AND of R1 and R2
```
Another type of command is **Memory Addressing** which comes in 3 flavors
*Direct Addressing* Which is used to directly address memory locations
```
LOAD R1,67 // R1 <- Memory[67]
// Or assume bar has address of Memory[67]
LOAD R1,bar // R1 <- Memory[67]
```

*Immediate Addressing* Used to load constant to a memory location
```
LOADI R1,67 // R1 <- 67
```

*Indirect Addressing* In this type of command, we are not directly coding memory address, instead we use memory location that holds address (like `c` pointers)
```
// Translation of x = foo[j] or x = *(foo+j);
ADD R1,foo,j // R1 <- foo + j
LOAD* R2, R1 // R2 <- Memory[R1]
STR R2, x // x <- R2
```
**Flow Control**
![image](images/flow-control.png)


## Hack Machine Language Specification

### Overview
The Hack computer is a von Neumann platform. It is a 6-bit machine, consisting of a CPU, two separate memory modules serving as instruction memory and data memory, and two  memory-mapped I/O devices: a screen and a keyboard.

**Memory Address Spaces** There are two different memory spaces. ROM and RAM. ROM is used to store program and RAM is used to store data.

**Registers**
There are three registers `A, D and M` `A` is a register that stores aboth address and data depends on instruction context.
`D` stores data. `M` stores a value of a memory location whose address is in `A`
If we need to access data in memory location 512, then first we need to loadd that address in A and then use M which now have data in 512
```
@512 // A points to RAM[512]
D=M // M is value of RAM[512]
```

### The A-Instruction
It is used to store 2 types of 15 bit value (most significant bit is not used)
When we say `@100` we are storing the constant 100 in A register. When we say `@sum` we are referring to some memory location. When use it for first time, it is like variable declaration. It finds some free memory space and tag it as `sum`. In subsequent uses, it refers to the value stored in that memory space.

### The C Instruction
This code specifies three operations 
1. What to compute
2. Where to store the computed value
3. What to do next
`dest = comp;jump` *dest* and *jump* are optional
![image](images/c-instruction.png)

The 7 `comp` bits can represent 128 operations
And `dest` as follows
![image](images/c-instruction-dest.png)

And `jump` as follow
![image](images/c-instruction-jump.png)

**Conflicting Uses of the A Register** As was just  illustrated, the programmer can use the A register to select either a data memory location for a subsequent  C-instruction involving M, or an instruction memory location for a subsequent C-instruction involving a jump. Thus, to prevent conflicting use of the A register, in well-written programs a C-instruction that may cause a  jump (i.e., with some non-zero j bits) should not contain a reference to M, and vice versa.

### Symbols
Assembly commands can address memory locations either using constants or symbols

#### Predefined symbols
A special subset of RAM address can be specified using predefined symbols. There are 5 types of such symbols
1. *Virtual registers* R0 to R15 refers to RAM addresses 0 to 15
2. *Predefined Pointers* Symbols `SP, LCL, ARG, THIS and THAT` refers to RAM address 0 to 4. So 0 can be refered using SP and R0 and so on upto 4.
3. *I/O pointers* Display pixels are mapped to a block of memory space and Keyboard input are stored in a single register. Each of this are referred by `SCREEN` and `KBD`
4. *Label symbols* we can specify a memory address of an instruction using a user defined symbol called label. It is used in GOTO (jump) commands
5. *Variable symbols* a user defined symbol used to refer a memory location

### Input / Output Handling
#### Screen
In hack computer a display consist of 256 rows of 512 pixels per row. So we need 32 consecutive 16bit registers to represent a row. In total we need 8K memory space to present display pixels of 256x512

#### Keyboard
In Hack computer a single 16 bit register is used to store whatever key is pressed by user at a time.


# Computer Architecture
In this chapter we are going to build a minimal yet surprisingly powerful computer using the chips we created in last 4 chapters. Computer follow Von Neumann architecture which is the underlying design for almost all modern computers.

The "Hack" computer is simple in the sense it can be constructed in few hours using previously built chips

It is also powerful, in the sense it can illustrate key operating principles and hardware elements of any digital computer

## Background

### The Stored Program Concept
Stored program concept is formulated independently by several mathematicians in the 1930s. It is the base for digital computer's versatility and make it perform different tasks such as games to word processing to scientific calculations with finite hardware.

### The Von Neumann Architecture.
Stored program concept is a key element in both abstract and practical computer models. `The turing machine` is an abstract artifact describing a simple computer Where as 'von neumann machine` is a practical architecture and conceptual blueprint for allmost all modern computers.

The von Neumann architecture has memory which is used to store program and data. CPU which is responsible with interacting with memory, input and output devices as well as execute stored program

### Memory
In von Neumann architecture memory holds two types of information. Data and programming instructions

**Data memory** High level programming languages manipulate data using variables, array and objects. When translated into machine language these become series of bits and stored in data memory

**Instruction memory** High level programming commands are translated to machine language and represented in binary. These bits are encoded desired operation which is decoded and executed by CPU

### Central Processing Unit
CPU, reads instruction from memory, executes them. Performs operations as instructed by program instruction, reads and writes values to memory, changes program flow, if needed. These are done using three main hardware elements
- ALU
- a set of registers
- a control unit
CPU operates in a repeated loop. Fetch instruction, decode and execute it. Repeat again for next instruction and so on.


**Arithmetic Logic Unit**
Responsible for performing all the low level arithmatic and logical operations

**Registers**
ALU is designed to carry out simple calculations. Instead of storing the result of such calculations in RAM (which is time consuming to access and read), CPU uses registers which holds a single word.

**Control Unit**
A computer instruction can be 16, 32 or 64 bit wide depending on architecture. Before executing, it must be decoded (separate operation, designation, etc) This is done by Control unit.

### Registers
As said earlier, memory access is slow. Because CPU as to tell memory address which needs to travel in address bus, then memory access logic selects memory register and place data in data bus and it travels to CPU.

Registers are quick as it resides within CPU. No need to set request via address bus and receive data via data bus.

**Data registers** used as short term memory to store results.

**Addressing registers** Used to store memory address and use it to read and write data from RAM

**Program counter register**
Keeps track of address of next instruction to be fetched and executed. Content of PC changes either incrementally or jump to specific instruction depends on result of currely executed instruction

### Input and Output
Input and Output devices are represented using memory mapping technique. For example, each pixel in display in represented by a memory register. Also pressed key or mouse position is stored in binary form in register. Like wise many types of input and output devices and its information (binary data to world information) are mapped to memory locations. 


