---
layout: default
title: "Problem Set Week 2"
permalink: /50002/PS2/
---

{::options parse_block_html="true" /}
{% include toc.html %}
{::options parse_block_html="false" /}

This page contains all practice questions that constitutes the topics learned in <ins>Week 2</ins>: **CMOS Technology** and **Logic Synthesis**. 

Each topic's questions are grouped into **three** categories: basic, intermediate, and challenging. You are recommended to do all basic problem set before advancing further. 

# CMOS Technology
You can refer to the notes <a href="https://natalieagus.github.io/50002/cmos_technology.html" target="_blank">here</a> if you need to revise. 

### Combinational Logic Timing (Basic)

Consider the following combinational logic device.
<img src="https://www.dropbox.com/s/hsjn3h2yy149dxx/Q10.png?raw=1" width="70%" height="70%">

 Each logic gate has the same:
 - Propagation delay,  t_{pd}= 2ns, 
 - Contamination delay, t_{cd}=1ns

Compute the **overall** propagation delay and contamination delay for the circuit. 

{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

>Overal  $t_{pd}$ = 6ns, $t_{pd​}$ = 6ns  (counting paths from the AND gate, OR gate, and XOR gate). 
>
>Overall  $t_{cd}$ = 1ns, $t_{cd}$ ​= 1ns  (counting the shortest path from XOR gate only). 

</details>
<br/>
{::options parse_block_html="false" /}

### Tracing CMOS Circuit (Basic)

**Draw** the truth table for the following CMOS circuitry:

<img src="https://www.dropbox.com/s/crosfbfiqf1iueg/Q11.png?raw=1"  width="30%" height="30%">


{::options parse_block_html="true" /} 
<details> 
<summary markdown="span">Show Answer</summary> 

>$$ \begin{matrix}
A & B & C & OUT \\ \hline 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 1 \\ 0 & 1 & 0 & 1 \\ 0 & 1 & 1 & 1 \\ 1 & 0 & 0 & 1 \\ 1 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 \\ 1 & 1 & 1 & 0 \\ 
\hline
\end{matrix}
$$
</details>  
<br/>  
{::options parse_block_html="false" /}



### Full Adder Timing Analysis (Intermediate)

Refer to the FA circuitry below:
<img src="https://www.dropbox.com/s/nqfbozivm2mdrvf/Q12.png?raw=1" width="50%" height = "50%">

Answer the following questions:
1. **Compute** the  $t_{pd}$​  and  $t_{cd}$ of the full adder above.
2.  If we were to put several of these FAs to form an 8-bit ripple-carry adder as shown, **compute** the $t_{pd}$ and $t_{cd}$  of an 8-bit ripple-carry adder made of 8 of these FA circuits. 

	<img src="https://www.dropbox.com/s/y30lar5nypnbh52/Q13.png?raw=1" width="70%" height = "70%">


	*Hint: In the figure,  $C_0$​  is assumed to be **grounded** for this particular **instance**, so this sample device can only add two numbers and not subtract them.*

	*However, is the computation of $t_{pd}$​  and  $t_{cd}$ of an 8-bit ripple carry adder usage specific?* 


{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

>1. The $t_{pd}$ is 1.8 and the $t_{cd}$  is 0.3 for a single FA. 
>2. For the 8-bit ripple-carry adder, we do not have an input  $C_0$ as it is grounded However the $t_{cd}$​  is *still* 0.3 as the specification of contamination delay is **not** usage specific. Its  $t_{pd}$  is 8 times bigger than a single FA $\rightarrow$  $t_{pd}$= 14.4. 
> 
> However if the question is asking for the  $t_{cd}$  of  **this**  particular device with no  $C_0$ input terminal at all (and not generic 8-bit ripple carry adder), then the answer is  **0.6ns**  since there's no  $C_0$. 
</details>
<br/>
{::options parse_block_html="false" /}

### Combinational Construction Rules (Challenging)

During lecture, we learned a first set of principles that define a combinational device. A combinational device is a circuit element that has:
1.  One or more digital inputs
2.  One or more digital outputs
3.  A **functional** specification that details the value of each output for every possible combination of valid input values
4.  A **timing** specification consisting (at minimum) of an upper bound  $t_{pd}$  on the required time for the device to compute the specified output values from an arbitrary set of stable, valid input values.

We also learned a second set of rules, that a set of interconnected elements ***is*** a combinational device if:
1.  **Each** circuit element is combinational
2.  Every input is connected to exactly **one** output or to some vast supply of 0's and 1's. 
	> *Note: read this carefully. This does NOT mean that a combinational device must just have one output and one input. **This means that *for each input of a combinational device*, it is connected to *exactly ONE output* of the "previous" device.*** 
3.  The circuit contains **no** directed cycles

In this problem, we ask you to think carefully about why these rules work - in particular, why *an acyclic circuit of combinational devices,* constructed according to the second principle, is itself a combinational device as defined by the first. 

Consider the following 2-input acyclic circuit whose two components, A and B, are each combinational devices. You may assume for the following that every input and output is a logical 0 or 1. 

<img src="https://www.dropbox.com/s/divqzx422azog4h/Q1.png?raw=1"  width="70%" height = "70%">


The propagation delay for each device is specified in nanoseconds. 

The **functional specifications for each component** are given as truth tables detailing output values for each combination of inputs, where $A _{a_0, a_1}$ denotes the output from device A, and $B _{a_0, a_1}$ denotes the output from device B:

$$\begin{matrix}
a_0  & a_1  &  A _{a_0, a_1}  &  b_0​  &  b_1  & B_{b_0, b_1}\\ 
\hline \\
0 & 0 & 1 & 0 & 0 & 0\\ 
0 & 1 & 0 & 0 & 1 & 0\\
 1 & 0 & 0 & 1 & 0 & 0\\ 
 1 & 1 & 1 & 1 & 1 & 1\\
 \hline 
\end{matrix}$$


**Answer** the following questions,

1.  Give a truth table for the **overall** acyclic circuit, i.e. a table that specifies the value of z for each of the possible combinations of input values on x and y.

2.  **Describe** a general procedure by which a truth table can be computed for each output of an arbitrary acyclic circuit containing only combinational components. *Hint : construct a functional specification to each circuit node.* 

3.  **Specify a propagation delay** (the upper bound required for each combinational device) for the circuit.

4.  **Describe** a general procedure by which a propagation delay can be computed for an arbitrary acyclic circuit containing only combinational components. \textit{Hint: add a timing specification to each circuit node}.

5.  Do your general procedures for computing functional specifications and propagation delays work if the restriction to acyclic circuits is relaxed (lifted)? **Explain**.



{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

>1. The truth table is as follows:
>
>$$\begin{matrix}
x & y & z \\ 
\hline 
0 & 0 & 0 \\ 0 & 1 & 0 \\ 1 & 0 & 0 \\ 1 & 1 & 1 \\ \hline \end{matrix}$$
>2. We can construct the truth table from left to right, i.e: solve the truth table for each component from the leftmost all the way to the rightmost, one by one.
>
>3. The total propagation delay is the sum of each device's (A and B) propagation delay: 3 + 2 = 5.
>4. One has to find the **longest** path from (any) input to (any) output to find the **total** propagation delay of the combinational circuit.
>5. No, the signal can **propagate** **back** in the circuit so using the *longest* path to calculate  $t_{pd}$  is not applicable anymore. 
</details>
<br/>
{::options parse_block_html="false" /}

# Logic Synthesis

You can refer to the notes <a href="https://natalieagus.github.io/50002/logic_synthesis.html" target="_blank">here</a> if you need to revise. 

### CMOS Circuit Boolean Expression (Basic)



<img src="https://www.dropbox.com/s/x1surj7fotwv45a/Q9.png?raw=1"  width="50%" height = "50%">

1. **Draw** the truth table of the CMOS circuit above. 
2. What is the **boolean** expression for the CMOS circuit shown?


{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

>1.  The truth table of the CMOS circuit contains 16 lines since theres $2^4$ possible input combinations and 1 possible output bit:
$$\begin{matrix} 
A & B & C & D & F \\ \hline 0 & 0 & 0 & 0 & 1 \\ 0 & 0 & 0 & 1 & 1 \\ 0 & 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 1 & 1 \\ 0 & 1 & 0 & 0 & 1 \\ 0 & 1 & 0 & 1 & 0 \\ 0 & 1 & 1 & 0 & 0 \\ 0 & 1 & 1 & 1 & 0 \\ 1 & 0 & 0 & 0 & 1 \\ 1 & 0 & 0 & 1 & 1 \\ 1 & 0 & 1 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 \\ 1 & 1 & 0 & 0 & 1 \\ 1 & 1 & 0 & 1 & 0 \\ 1 & 1 & 1 & 0 & 1 \\ 1 & 1 & 1 & 1 & 0 \\ \hline \end{matrix}$$
>2. $F = \overline{A(B+C)D}$

</details>
<br/>
{::options parse_block_html="false" /}



  
  
  

### Combinational Circuit's Functional Specs (Basic)

  
Consider the following circuit that implements the 2-input function $H(A,B)$:

<img src="  https://www.dropbox.com/s/2vy52yuzs24xfc4/Q2new.png?raw=1"  width="50%" height = "50%">

1. Give the truth table for $H$.
2. Give a sum-of-products expression that corresponds to your truth table.

$$\begin{matrix}
A & B & H \\
\hline
0 & 0 & 1\\
0 & 1 & 1 \\
1 & 0 & 0 \\
1 & 1 & 1\\
\hline
\end{matrix}
$$
\caption{}

\end{table}

  

We begin by finding the expression of the topmost two circuits:, and applying de Morgan's law:

\begin{align}

\overline{A + \overline{B}} = \overline{A}B

\end{align}

  

Then find the expression of the next pair, which is $AB$. We combine this with the above using a NOR gate and reduce the result,

\begin{align}

\overline{\overline{A}B + AB} = \overline{B}

\end{align}

  

Finally, we find the expression for the bottom two pairs, which is simply $A+B$. Combine this with the above expression, we reduce and apply de Morgan's law:

\begin{align}

\overline{(A+B)\overline{B}} = \overline{A \overline{B} + B \overline{B}} = \overline{A\overline{B}} = \overline{A} + B

\end{align}

\fi

  

1. Using the information below, what are the $t_{cd}$ and $t_{pd}$ of the circuit?

  

\includepic{0.6}{Q3.png}

  

\ifanswers

\beginsol

The contamination delay is the shortest path: NR2 + NR2 + ND2 = 5 + 5 + 5 = 15ps. The propagation delay is the longest path: AN2 + NR2 + ND2 = 50 + 30 + 30 = 110ps.

\fi

  
  
  

### Warm Up -- Boolean Algebra

  

Given the following truth table,

\begin{table}[h]

\centering

\begin{tabular} {c|c|c|c}

A & B & C & OUT \\\\

\hline

0 & 0 & 0 & 1 \\\\

0 & 0 & 1 & 1 \\\\

0 & 1 & 0 & 1 \\\\

0 & 1 & 1 & 0 \\\\

1 & 0 & 0 & 1 \\\\

1 & 0 & 1 & 1 \\\\

1 & 1 & 0 & 1 \\\\

1 & 1 & 1 & 0 \\\\

\hline

\end{tabular}

\caption{}

\end{table}

  

Choose all the correct Boolean expression of this circuit:

  
  

1. $OUT = \bar{C} + \bar{B}$

1. $OUT = \bar{A} \cdot \bar{B} + A \cdot \bar{B} + B \cdot \bar{C}$

1. $OUT = \bar{A} \cdot \bar{C} + A \cdot B \cdot \bar{C} + \bar{B}$

1. $OUT = \bar{A} \cdot B + A \cdot B \cdot \bar{C} + \bar{B}$

  
  

\ifanswers

\beginsol

(a), (b), and (c) are all equivalent and represents the truth table. \textit{Hint: express the table in terms of sum of products first and simplify the expression.}

\fi

  

### Warm up -- Reading ROM

  

\includepic{0.4}{rom}{}

What is the the sum-of-products for the following ROM (Read Only Memory)?

  

\ifanswers

\beginsol

$Y = \bar{A}\bar{B}\bar{C} + \bar{A}BC + A \bar{B} C+ AB\bar{C}$. This expression can be computed easily after you create a truth table first out of the ROM.

\fi

  
  

\newpage

  

### Half-Adder Implemented as ROM

  

\includepic{0.4}{farom.png}{}

Take a look at the figure above. Which of the above ROM represents the functionality of a half adder?

  

\ifanswers

\beginsol

  

ROM [3] represents half-adder functionality. Y's output shows a XOR(A,B) while Z's output shows an AND(A,B). Hence this make Y to be the SUM output and Z to be the CARRY output.

  

\fi

\newpage

### CMOS Gate Analysis

  

The following diagram shows a schematic for the pulldown circuitry for a particular CMOS gate:

  

\includepic{0.5}{Q1.png}

  
  
  

1. What is the correct schematic for the pullup circuitry?

\ifanswers

\beginsol

The output for the pullup circuitry is the inversion of the output of the pulldown circuitry, $\overline{(A+B) C + D} = (\overline{A} \text{ }\overline{B} + \overline{C}) \overline{D}$. The plot is located at the first diagram on the next page.

  

\includepic{0.7}{A1.png}

\fi

  

1. Assuming the pullup circuitry is designed correctly, what is the logic function implemented this gate?

  

\ifanswers

\beginsol

The output for the gate is the output of the pullup circuitry above: $\overline{(A+B) C + D}$.

\fi

  

1. Assuming the pullup circuitry is designed correctly, when the output of the CMOS gate above is a logic "0", in the steady state what would we expect the voltage of the output terminal to be? What would be the voltage if the output were a logic "1"?

  

\ifanswers

\beginsol

The voltage of the output terminal at "0" steady state is 0 (GND). The voltage of the output terminal at "1" steady state is VDD's voltage.

\fi

  
  
  

### Simplifying a Rather Complicated Boolean Expression

  

Simplify the following expression:

~\\~\\

$Y = AB \bar{C} \bar{D} + AB \bar{C}D + \bar{A} \bar{B}CD + \bar{A}BCD + ABCD + A\bar{B}CD + \bar{A}\bar{B}C \bar{D} + ABC \bar{D} + A\bar{B}C \bar{D}$.

  

\ifanswers

\beginsol

The final simplified form is $Y = AB + CD + \bar{B}C$. The steps are as follows:

  

\begin{align}

Y &= AB \bar{C} \bar{D} + AB \bar{C}D + \bar{A} \bar{B}CD + \bar{A}BCD + ABCD \\\\

& + A\bar{B}CD + \bar{A}\bar{B}C \bar{D} + ABC \bar{D} + A\bar{B}C \bar{D}\\

&= AB\bar{C} + \bar{A}CD + ACD + \bar{B}CD + ABC\bar{D}\\

&= CD + AB\bar{C} + \bar{B}CD + ABC\bar{D}\\

&= C(D + \bar{B} \bar{D}) + AB(\bar{C} + C\bar{D} )\\

&= C(D + \bar{B} ) + AB(\bar{C} + \bar{D} )\\

&=CD + C\bar{B} + AB(\overline{CD} )\\

&= CD + C\bar{B} + AB

\end{align}

\fi

  

### CMOS Gate Design

  

Anna Logue, a circuit designer who missed several early 6.004 lectures, is struggling to design her first CMOS logic gate. She has implemented the following circuit:

\includepic{0.6}{Q2.png}

Anna has fabricated 100 test chips containing this circuit, and has a simple testing circuit which allows her to try out her proposed gate statically for various combinations of the A and B inputs. She has burned out 97 of her chips, and needs your help before destroying the remaining three. She is certain she is applying only valid input voltages, and expects to find a valid output at terminal C. Anna also keeps noticing a very faint smell of smoke.

  
  
  

1. What is burning out Anna's test chips? Give a specific scenario, including input values together with a description of the failure scenario. For what input combinations will this failure occur?

  

\ifanswers

\beginsol

When $A=0, B=1$ or $A=1, B=0$, then there's an open connection between VDD and GND. This caused the gate to short circuit, and hence its burning out.

\fi

  

1. Are there input combinations for which Anna can expect a valid output at C? Explain.

\ifanswers

\beginsol

Yes, when $A=1, B=1$ then $C=0$, or $A=0, B=0$, then $C=1$. This is when the pullup and pulldown circuit aren't both ON at the same time.

\fi

  

1. One of Anna's test chips has failed by burning out the pullup connected to A as well as the pulldown connected to B. Each of the burned out FETs appears as an open circuit, but the rest of the circuit remains functional. Can the resulting circuit be used as a combinational device whose two inputs are A and B? Explain its behavior for each combination of valid inputs.

  

\ifanswers

\beginsol

No. When $A=1, B=0$, the circuit will burn out again, since the pullup and pulldown will be active, thus burning out the circuit. Also, the output is not defined when $A=0, B=1$, since neither the pullup or pulldown are active.

\fi

  

1. In order to salvage her remaining two chips, Anna connects the A and B inputs of each and tries to use it as a single-input gate. Can the result be used as a single-input combinational device? Explain.

  

\ifanswers

\beginsol

Yes. It exhibits the behavior of an inverter, i.e: A and B are connected to the same $V_{IN}$.

\fi

  
  

### Sum Of Products

  

A certain function F has the following truth table:

  

\includepic{0.6}{Q3.png}

  
  

Answer the following questions based on the truth table:

  
  

1. Write a sum-of-products expression for F

  

\ifanswers

\beginsol

$\overline{A}\text{ }\overline{B}\text{ }\overline{C} + \overline{A}BC + A \overline{B}\text{ }\overline{C} + A \overline{B}C + ABC$.

\fi

1. Write a minimal sum-of-products expression for F. Show a combinational circuit that implements F using only INV and NAND gates.

\ifanswers

\beginsol

The minimal sum of products is : $\overline{B}A + \overline{B} \text{ } \overline{C} + BC$. You can draw a combinational circuit of this by adding OR gate for every +, inverter, and AND gate for every pair of input in the minimal sum of products.

\fi

  

1. Implement F using one 4-input MUX and inverter.

  

\ifanswers

\beginsol

If we use A and B as the select inputs for the MUX then the four data inputs of the MUX should be tied to one of "0" (ground), "1" (Vdd), "C" or "not C". For this function the following is the correct schematic. Note that by changing the connections on the data inputs we could implement any function of A, B and C.

\includepic{0.4}{Q4.png}

  

\fi

1. Write a minimal sum-of-products expression for NOT(F).

\ifanswers

\beginsol

We can just write equations for patches that cover the '0's in the table above, and then reduce the expression into: $\overline{F} = B \overline{C} + \overline{A} \text{ } \overline{B} C$

\fi

  
  
  

### Gates and Boolean Equations

  

For the questions below, refer to the figure:

  

\includepic{0.5}{Q4new.png}{}

  
  
  

1. Show the Boolean equation for the function F described by the circuit on the left.

\ifanswers

\beginsol

$\overline{A}B + A\overline{C}D + A \overline{B}C$

\fi

  

1. Consider the circuit shown on the right. Each of the control inputs, $C_0$ through $C_3$, must be tied to a constant, either 0 or 1. What are the values of $C_0$ through $C_3$ that would cause F to be the \textit{exclusive} OR (XOR) of A and B?

  

\ifanswers

\beginsol

The truth table for A XOR B is: $A=0, B=0, F =0$, $A=0, B=1, F=1$, $A=1, B=0, F=1$, $A=1, B=1, F=0$. In class, we know that XOR is equivalent to $A\overline{B} + \overline{A}B$. Since all the gates in the first column of the circuit on the right is an AND, setting any $C_i$ coefficient to 0 'disables' the gate, i.e: produces a zero. Hence, we can set $C_1$=1 and $C_2=1$ to follow the aforementioned boolean expression for XOR gate, and set $C_0$ and $C_3$ to zero to disable the rest if the AND gates.

  

\fi

  

1. Can any arbitrary Boolean function of A and B be realized through appropriate wiring of the control signals C0 through C3?

\ifanswers

\beginsol

Yes, the circuit on the right represents the sum of products, which can realise any boolean function, but it is not necessarily the smallest or the most efficient to build.

\fi

  

1. Give a sum-of-products expression for each of the following circuits:

\includepic{0.3}{Q5new.png}{}

\ifanswers

\beginsol

\begin{enumerate}

1. $F = \overline{\overline{\overline{A} {B}} \cdot \overline{C}B} = \overline{A}B + \overline{\overline{C}B}=\overline{A}B + \overline{B} + C$

1. $F = \overline{(A+\overline{C})(B+\overline{C})} = \overline{(A+\overline{C})} + \overline{(B+\overline{C})} = \overline{A}C + \overline{B}C$

1. $F = \overline{A+\overline{C}} + \overline{\overline{B}+C} = \overline{A}C + B\overline{C} $

1. $F = \overline{A}B+A\overline{C}D + A\overline{B}C$

1. $F = \overline{A}\text{ }\overline{D} + BC + B\overline{D}$

  
  

\fi

  

\item Give a canonical sum-of-products expression for the Boolean function described by each truth table shown in Fig. 10.

  

\includepic{0.3}{Q6.png}

\ifanswers

\beginsol

The canonical sum-of-products expression only take into account the rows where F is 1. So for the table on the left,

\begin{align}

\overline{A}\text{ } \overline{B} \text{ }\overline{C} + A \overline{B} \text{ }\overline{C} + A \overline{B} C + ABC

\end{align}

For the table on the right,

\begin{align}

\overline{A} B C + A \overline{B} C + AB\overline{C} + ABC

\end{align}

\fi

  

\item We've seen that there are a total of sixteen 2-input Boolean functions: AND, OR, XOR, NOR, etc. How many 5-input Boolean functions are there?

  

\ifanswers

\beginsol

There will be $2^{2^5}$ 5-input boolean functions.

\fi

  
  

\end{enumerate}

\newpage

### Reading Karnaugh's Map

  

Given the following Karnaugh's Map, write the **simplified** boolean equation.

  

\begin{table}[h]

\centering

\begin{tabular}{c|c|c|c|c}

& $\bar{A}$  $\bar{B}$ & $\bar{A} B$ & $A$$B$ & $A$$\bar{B}$  \\\\

\hline

$\bar{C}\bar{D}$ & 1 & 0 & 0 & 1 \\\\

$C\bar{D}$ & 1 & 0 & 0 & 1\\

$CD $ & 0 & 0& 1 & 1\\

$\bar{C}D$ & 1 & 0 & 1 & 1\\

\hline

\end{tabular}

\caption{}

\end{table}

  

\ifanswers

\beginsol

$AD + \bar{B}\bar{C} + \bar{B} \bar{D}$, obtained from "three" boxes: on the lower right corner (row 3 and 4, with column 3 and 4), on the sides (row 1 and 2, with column 1 and 4), and on the four corners (row 1 col 1, and row 1 col 4, and row 4 col 1, and row 4 col 4).

\fi

\newpage

### Universal Gates

  

Use NAND gates to redraw the circuit. Use as few NAND gates as possible.

  

\includepic{0.6}{Q7}{}

  

\ifanswers

\beginsol

\includepic{0.5}{Q8}

\fi

  
  

\newpage

### Challenge -- FPGA

  

The Xilinx 4000 series field-programmable gate array (FPGA) can be programmed to emulate a circuit made up of many thousands of gates; for example, the XC4025E can emulate circuits with up to 25,000 gates. The heart of the FPGA architecture is a configurable logic block (CLB) which has a combinational logic subsection with the following circuit diagram:

\includepic{0.5}{Q5}

  

There are two 4-input function generators and one 3-input function generator, each capable of implementing an arbitrary Boolean function of its inputs.

The function generators are actually small 16-by-1 and 8-by-1 memories that are used as lookup tables; when the Xilinx device is "programmed" these memories are filled with the appropriate values so that each generator produces the desired outputs. The multiplexer select signals (labeled "Mx" in the diagram) are also set by the programming process to configure the CLB. After programming, these Mx signals remain constant during CLB operation.

The following is a list of the possible configurations. For each configuration indicate how each the control signals should be programmed, which of the input lines (C1-C4, F1-F4, and G1-G4) are used, and what output lines (X, Y, or Z) the result(s) appear on.

  
  
  

1. An arbitrary function F of up to four input variables, plus another arbitrary function G of up to four unrelated input variables, plus a third arbitrary function H of up to three unrelated input variables.

  

\ifanswers

\beginsol

Let X = F(F1, F2, F3, F4), Z = G(G1, G2, G3, G4), Y = H(C1, C2, C3). The necessary control signals are:

  

\begin{enumerate}

1. MA = 1

1. MB = 1

1. MC = 0 (select C1)

1. MD = 1 (select C2)

1. ME = 2 (select C3)

  
  

\fi

\item An arbitrary single function of five variables.

  

\ifanswers

\beginsol

Let Y = F(A1, A2, A3, A4, A5). This can be implemented using both 4-input logic functions, and selecting between the two outputs with the 3-input logic function.

  
  

1. Z=f(A1, A2, A3, A4, 0),

1. X=f(A1, A2, A3, A4, 1),

1. Y= Z if A5=0, else Y=X

  

So Z is calculating F for the case when A5 = 0, X is calculating F for the case when A5 = 1, and Y is selecting between X and Z with a multiplexer function. A1-A4 represents F1-F4 and G1-G4 (they're connected to the same 4 inputs) and A5 represents C1. The necessary control signals are:

  
  
  

1. MA = 0

1. MB = 0

1. MC = X (value doesn't matter)

1. MD = X (value doesn't matter)

1. ME = 0 (select C1)

  

\fi

\item An arbitrary function of four variables together with some functions of six variables. Characterize the functions of six variables that can be implemented.

  
  

\ifanswers

\beginsol

Let Z = G(G1, G2, G3, G4) : any function of 4 variables.

  
  
  

1. X = F(F1, F2, F3, F4)

1. Y = H(C1, C2, X) = H(C1, C2, F(F1, F2, F3, F4))

  

The functions of six variables which can be implemented (along with the 4-variable function) are all those functions that can be re-written as a function of 3 variables. The inputs to this function of three variables must be 2 of the original variables and some function of the remaining four variables. The necessary control signals are:

  
  

1. MA = 0

1. MB = 1

1. MC = X (value doesn't matter)

1. MD = 0 (select C1)

1. ME = 1 (select C2)

  

\fi

\item Some functions of up to nine variables. Characterize the functions of up to nine variables that can be implemented.

  

\ifanswers

\beginsol

Let:

  
  
  

1. X = F(F1, F2, F3, F4)

1. Z = G(G1, G2, G3, G4)

1. Y = H(C1, X, Z) = H(C1, F(F1, F2, F3, F4), G(G1, G2, G3, G4))

  

The functions of nine variables that can be implemented are all those functions that can be re-written as a function of 3 variables. The inputs to this three-variable function will be one of the original variables, plus two separate functions of 4 variables (these two 4-variable functions will have the remaining 8 original variables as inputs).

  
  

1. MA = 0

1. MB = 0

1. MC = X (value doesn't matter)

1. MD = X (value doesn't matter)

1. ME = 0 (select C1)

  
  

\fi

\item (Optional challenge) Can every function of six inputs be implemented? If so, explain how. If not, give a 6-input function and explain why it can't be implemented in the CLB.

  

\ifanswers

  

\beginsol

  

The functions of 6 variables which we can implement must be of the form:

  

\[Y = y(C1, C2, f(F1,F2,F3,F4))

\]

or of the form:

\[

Y = y(C1, f(F1, F2, F3, F4), g(G1, G2, G3, G4))

\]

(this second function will have some overlap between C1, F1-4, and G1-4; some variables will be connected to multiple inputs) Essentially, the functions we are able to implement are only those for which we can factor a set of 4 variables out of the equation. For example, the following function cannot be implemented by the CLB:

\[

Y = A1A2A3A4A5 + A1A2A3A4A6 + A1A2A3A5A6 + A1A2A4A5A6 +

\]

\[ A1A3A4A5A6 +A2A3A4A5A6

\]

This function cannot be broken down into either of the forms mentioned above.

  
  
  
  
  

\fi

\end{enumerate}
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MTczNjMyMDgsLTg0NzczNjUyMiwyNz
IwNzI4MDQsLTYwMjg1NDI5LC0xMTczMDE3ODU3LDIwMTc0OTkz
NjIsMjEwMzMzODcwMSwtOTAyNDQ5NjE2LDEwMjUzNjQ1ODRdfQ
==
-->