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
