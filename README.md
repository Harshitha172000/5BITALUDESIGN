# 5BITALUDESIGN
ARITHMETIC LOGIC UNIT LAYOUT DESIGN

EC302: VLSI LAB PROJECT REPORT
submitted by

Harshitha S (181EC216)
 
under the guidance of
                                            Dr Ramesh Kini

                 DEPARTMENT OF ELECTRONICS AND COMMUNICATION ENGINEERING
NATIONAL INSTITUTE OF TECHNOLOGY KARNATAKA
SURATHKAL, MANGALORE - 575025

         
                                                             December 22, 2020


TABLE OF CONTENTS

Sl no
TITLE
Pg no
1
INTRODUCTION
3
2
DESIGN OBJECTIVES
3
3
BLOCK CIRCUIT OF DESIGN
4
4
5-BIT ALU DESIGN DESCRIPTION
4
5
TESTING- IRSIM SIMULATION RESULTS
8
6
CONCLUSION
12


LIST OF FIGURES AND TABLES

Table1. Operations performed by 5bit ALU
Fig1. ALU block circuit of design
Fig2. Layout of adder/subtractor
Fig3. Layout of 5bit Multiplier
Fig4. Layout of 5bit ALU
Table2. Select lines for ALU operations
Table3. Description of labels used in layout
Fig5. Irsim results for select line 10
Fig6. Irsim results for select line 11
Fig7. Irsim results for select line 00.
Table 4. Tabulation of delay, power and area.
 

INTRODUCTION

Arithmetic Logic Unit (ALU) is a digital circuit used to perform arithmetic  and logic operations. It is a fundamental building block of the central processing unit (cpu) of a computer. Most of the operations of the CPU are performed by either one or two ALUs. So ALU is a very important part of the CPU and it's very important to make sure that the calculations done by ALU are accurate. If we look at ALU from designers and fabrication point of view the main challenge is to minimize the space occupied by the hundreds of transistors and wind the entire sub-blocks of ALU into a single unit and thus make design compact.


DESIGN OBJECTIVES

The main objective of this project is to design a 5bit ALU layout which performs addition, subtraction and multiplication of two 5bit numbers. In this design I have implemented 5bit ALU which can perform the following listed operations. Given A and B are two 5-bit numbers.

Addition
A + B
Subtraction
A - B
Multiplication
A * B
Inverting
A`
                        Table1. Operations performed by 5bit ALU

These are the operations performed by the 5 bit ALU. The subunits of ALU like adder, inverter, multiplier were first designed; later all these operations were integrated into a single layout using mux.




BLOCK CIRCUIT OF DESIGN


Fig1. ALU block circuit of design

As shown in figure 1, ALU has different sub-blocks like adder/subtractor, multiplier or inverter which on multiplexing works as a single ALU unit. To minimize space adder and subtractor both can be clubbed into a single design block whose operation can be controlled by Carry in (Cin).


5-BIT ALU DESIGN DESCRIPTION

Different sublocks of ALU are controlled using a select line. Subunits of ALU are as follows:
Adder/Subtractor
Multiplier
Inverter






Adder/Subtractor

This sub unit performs addition or subtraction operation on two 5bit inputs A and B. At a time either one of the operations can be done. If Cin=0, addition is performed and if Cin=0, subtraction is executed. The layout design of the adder subtractor is shown below. The design acts as both adder and subtractor due to the XOR of input B with Cin which is then applied to 5bit Full adder and thus acts as Adder-Subtractor.

            
Fig2. Layout of adder/subtractor
           
Metals M0 and M1 are used for intracell routing and M2, M3 are used   for over the cell routing. To optimise layout, rows are arranged to have common ground and VDD. There are about 200 transistors in this adder-subtractor circuit.





Multiplication

Multiplication of two 5bit inputs A and B is implemented using ripple carry adders. Layout of the multiplier is shown below. M0 and M1 are used for intra cell routing. M2 and M3 are used for intercell routing. Vias are used in layout which makes design more reliable. There are many transistors in the layout whose count is more than 840. To make layout compact, over the cell routing has to be done along with that rows are flipped upside down in order to have common VDD and ground.

 

Fig3. Layout of 5bit multiplier

Inverter

         Inverter intakes 5bit input A and converts it to  ~A. Inverter subunit layout is       
         very simple which can be done by simply dumping five inverters.

On combining all these subunits which can be done using multiplexer, complete ALU design can be implemented whose layout is shown in fig4.


Fig4. Layout of 5bit ALU

ALU has two select lines S0 and S1. Multiplexer selects one of the operations based on select line inputs.


S0 S1
   Operation
0 0
Multiplication
1 0
Inverter
1 1
Adder/Subtractor
Table2. Select lines for ALU operation









TESTING- IRSIM SIMULATION RESULTS OF ALU

Labels used in ALU layout are:
Input A 
Input B  
Carry in for adder/subtractor  
Result of adder/subtractor 
Result of Inverter 
Result of Multiplication
Select line
a4(MSB) a3 a2 a1 a0(LSB)
b4(MSB) b3 b2 b1 b0(LSB)
cin
cout s4 s3 s2 s1 s0
i4 i3 i2 i1 i0
p9 p8 p7 p6 p5 p4 p3 p2 p1 p0
x0 x1
Table3. Description of labels used in layout

I have written a cmd script file to check the results in irsim by giving inputs in the form of vectors. Step Size of 50 is given for all test cases. In irsim simulation, script file is called using os command. The following script file checks the inverter operation of ALU given inputs a4 a3 a2 a1 a0, outputs of inverter are i4 i3 i2 i1 i0. Select line for inverter operation is x0 =1 and x1= 0.

Script file to check inverter operation of ALU
stepsize 50
h Vdd
l Gnd
w a0 a1 a2 a3 a4 s0 s1 s2 s3 s4 p0 p1 p2 p3 p4 p5 p6 p7 p8 p9 i0 i1 i2 i3 i4
vector in x0 x1 a4 a3 a2 a1 a0
logfile outputs.log
set vlist {1010101 1011010 1011101 1011101 1011110}
foreach vec $vlist {setvector in $vec ; s}
logfile






IRSIM RESULTS OF ALU FOR SELECT LINE X0 X1 = 1 0

If selectline is 10 then inverter operation is performed. For the given input vectors of A in script file the corresponding output results are shown in figure 5.

Fig5. Irsim results for select line 10

Given below is the script file to check the addition and subtraction results of ALU. Given two inputs A(a4 a3 a2 a1 a0) and B(b4 b3 b2 b1 b0). Carry in (cin) is a control bit, based on this bit either addition or subtraction operation is computed. If Cin = 0, addition computed else subtraction is computed. In the script file, first two input  vectors will test addition whereas other two test vectors check subtraction. 

Script file to check adder/subtractor operation
stepsize 50
h Vdd
l Gnd
w a0 a1 a2 a3 a4 b0 b1 b2 b3 b4 i0 i1 i2 i3 i4 p0 p1 p2 p3 p4 p5 p6 p7 p8 p9 s0 s1 s2 s3 s4 cout cin
vector in x0 x1 cin a4 a3 a2 a1 a0 b4 b3 b2 b1 b0
logfile outputs.log
set vlist {1101010101101 1101101010010 1111110101101 1111110110011 }
foreach vec $vlist {setvector in $vec ; s}
logfile
IRSIM RESULTS OF ALU FOR SELECT LINE 11

If select line x0 x1 is 11 and cin is 0 then addition is computed. For x0 x1 = 1 1 and cin =1 then subtraction is performed. 


Fig6. Irsim results for select line 11.

To check the correctness of multiplication operation the below script is written. Select line 00 has to be chosen to perform multiplication operation.

Script file to check multiplication operation
stepsize 50
h Vdd
l Gnd
w a0 a1 a2 a3 a4 b0 b1 b2 b3 b4 i0 i1 i2 i3 i4 s0 s1 s2 s3 s4 p0 p1 p2 p3 p4 p5 p6 p7 p8 p9
vector in x0 x1 a4 a3 a2 a1 a0 b4 b3 b2 b1 b0
logfile outputs.log
set vlist {001101101011 001111101011 001100101111 001110110011 }
foreach vec $vlist {setvector in $vec ; s}
logfile

IRSIM RESULTS OF ALU FOR SELECT LINE 00

Four test input vectors are applied to test the multiplication operation. Figure 7 shows the irsim results.


Fig7. Irsim results for select line 00.

For some random test inputs delay and dynamic power consumption are:

Area of ALU design
53,54,698 sq microns
Worst case delay
15ns
Dynamic Power consumption when select line is 00
83nW
Dynamic Power consumption when select line is 11
50nW
Dynamic Power consumption when select line is q0
42nW
Table 4. Tabulation of delay, power and area.

CONCLUSION

A 5bit ALU was designed which comprises more than 1100 transistors. Metals used in design are M5, M4, M3, M2, M1, M0. Top level metals M5 and M4 are used in the long run connections. In short run connections metals M2 and M3 are used along with that vias were used to make design more reliable. In this design over the cell routing has been done to maintain design compactness. After layout design, the mag file is extracted and converted into a sim file. Using the sim file irsim simulation is done, along with that irsim command based script files were written to test the correctness of the layout design. With this tool all the ALU operations were verified.




