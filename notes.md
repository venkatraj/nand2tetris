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






