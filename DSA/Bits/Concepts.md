# **Bits and Bitwise Operators in Java** 

## **What is a Bit?**

A **bit** is the smallest unit of data in computing, representing either `0` or `1`. Everything in a computer—numbers, characters, and instructions—is ultimately stored in **binary** using bits.

## **Bitwise Operators**

Bitwise operators allow manipulation of individual bits within integers. Common bitwise operators include:

| Operator | Symbol | Example | Description|
|:---:|:---:|:---:|:---:|
| AND|&|5&3|Sets bits to 1 if both operands have 1 in the same position.|
|OR|\||5\|3|Sets bits to 1 if at least one operand has 1.|
|XOR|^|5^3|Sets bits to 1 if operands differ at that position.|
|NOT|~|~5|Flips all bits (1s become 0s, and vice versa).|
|Left Shift|<<|5<<1|<Shifts bits left, multiplying the number by 2.|
|Right Shift|>>|5>>1|Shifts bits right, dividing the number by 2 |


## **Common Uses of Bitwise Operators**

-   **Setting or Clearing Bits**: Used in memory-efficient programming.
-   **Checking Odd/Even Numbers**: `n & 1` checks if a number is odd (`1`) or even (`0`).
-   **Fast Multiplication/Division**: `n << 1` effectively multiplies `n` by `2`.
-   **Permissions and Flags**: Used in settings and configurations to store multiple values compactly.
-   **Bit Masks for Permissions:** Toggle specific bits for settings.
