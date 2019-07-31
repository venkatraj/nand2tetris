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
![image](../../truth-table-1.png)

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
