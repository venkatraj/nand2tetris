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