*5BIT ALU LAYOUT DESIGN DESCRIPTION*

Arithmetic Logic Unit (ALU) is a digital circuit used to perform arithmetic  and logic operations. It is a fundamental building block of the central processing unit (cpu) of a computer. Most of the operations of the CPU are performed by either one or two ALUs. So ALU is a very important part of the CPU and it's very important to make sure that the calculations done by ALU are accurate. If we look at ALU from designers and fabrication point of view the main challenge is to minimize the space occupied by the hundreds of transistors and wind the entire sub-blocks of ALU into a single unit and thus make design compact.

The main objective of this project is to design a 5bit ALU layout which performs addition, subtraction and multiplication of two 5bit numbers. In this design I have implemented 5bit ALU which can perform the following listed operations. Given A and B are two 5-bit numbers.

Addition(A + B),
Subtraction (A - B),
Multiplication (A * B),
Inverting (~A).

ALU has two select lines S0 and S1. Multiplexer selects one of the operations based on select line inputs.
0 0 Multiplication, 1 0 Inverter, 1 1 Adder/Subtractor.

I have used magic to design layout(.mag). To test design IRSIM is used. I have written a cmd script file to check the results in irsim by giving inputs in the form of vectors. Step Size of 50 is given for all test cases. During irsim simulation, script file is called using os command.

Labels used in layout:-  Input A : a4(MSB) a3 a2 a1 a0(LSB);  Input B : b4(MSB) b3 b2 b1 b0(LSB);  Carry in for adder/subtractor : cin;  Result of adder/subtractor : cout s4 s3 s2 s1 s0 ;  Result of Inverter : i4 i3 i2 i1 i0;  Result of Multiplication : p9 p8 p7 p6 p5 p4 p3 p2 p1 p0;  Select line : x0 x1;









