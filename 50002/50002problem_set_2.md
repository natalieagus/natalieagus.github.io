---
layout: default
title: "Problem Set Week 1"
permalink: /50002/PS2/
---

{::options parse_block_html="true" /}
{% include toc.html %}
{::options parse_block_html="false" /}

This page contains all practice questions that constitutes the topics learned in <ins>Week 2</ins>: **CMOS Technology** and **Logic Synthesis**. 

Each topic's questions are grouped into **three** categories: basic, intermediate, and challenging. You are recommended to do all basic problem set before advancing further. 

### Warm Up -- Combinational Logic Timing

Consider the following combinational logic. Each logic gate has the same propagation delay,  t_{pd}= 2ns, t_{cd}=1nstpd​=2ns,tcd​=1ns. Compute the overall propagation delay and contamination delay for the circuit. \includepic{0.6}{Q10}{}

\ifanswers \beginsol Overal  t_{pd} = 6nstpd​=6ns  (counting paths from the AND gate, OR gate, and XOR gate). Overall  t_{cd} = 1nstcd​=1ns  (counting the shortest path from XOR gate only). \fi

\newpage

### Warm Up -- Tracing CMOS Circuit

Draw the truth table for the following CMOS circuitry:

\includepic{0.4}{Q11}{}

\ifanswers \beginsol \begin{table}[h] \centering \begin{tabular} {c|c|c|c} A & B & C & OUT \\ \hline 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 1 \\ 0 & 1 & 0 & 1 \\ 0 & 1 & 1 & 1 \\ 1 & 0 & 0 & 1 \\ 1 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 \\ 1 & 1 & 1 & 0 \\ \hline \end{tabular} \caption{} \end{table}

\fi

\newpage

### Full Adder Timing Analysis

Refer to the FA circuitry below, \includepic{0.3}{Q12}{} Compute the  t_{pd}tpd​  and  t_{cd}tcd​  of the full adder above.~\ If we were to put several of these FAs to form an 8-bit ripple-carry adder as shown, **compute the  t_{pd**  and  t_{cd}tcd​  of an 8-bit ripple-carry adder made of 8 of these FA circuits}. In the figure,  C_0C0​  is assumed to be grounded for this particular instance, so this sample device can only add two numbers and not subtract them. \textit{However, is the computation of  t_{pd}tpd​  and  t_{cd}tcd​  of an 8-bit ripple carry adder usage specific?}. \includepic{0.45}{Q13}{} \ifanswers \beginsol  t_{pd}tpd​  is 1.8 and the  t_{cd}tcd​  is 0.3 for the FA. For the 8-bit ripple-carry adder, we do not have an input  C_0C0​  as it is grounded. However the  t_{cd}tcd​  is \textit{still} 0.3 as the specification of contamination delay is not usage specific. Its  t_{pd}tpd​  is eight times bigger than a single FA,  t_{pd} = 14.4tpd​=14.4.~\ ~\ However if the question is asking for the  t_{cd}tcd​  of  **this**  particular device with no  C_0C0​  at all (and not 8-bit ripple carry adder), then the answer is  **0.6ns**  since there's no  C_0C0​.

\fi

\newpage

### Combinational Construction Rules

In lecture, we learned two basic principles regarding the class of combinational devices. The first allows us to build a combinational device from, e.g., electronic components. A combinational device is a circuit element that has:

1.  one or more digital inputs
2.  one or more digital outputs
3.  a functional specification that details the value of each output for every possible combination of valid input values
4.  a timing specification consisting (at minimum) of an upper bound  t_{pd}tpd​  on the required time for the device to compute the specified output values from an arbitrary set of stable, valid input values.

while the second allows us to construct complex combinational devices from acyclic circuits containing simpler ones. A set of interconnected elements is a combinational device if:

1.  each circuit element is combinational
2.  every input is connected to exactly one output or to some vast supply of 0's and 1's
3.  the circuit contains no directed cycles

In this problem, we ask you to think carefully about why these rules work - in particular, why an acyclic circuit of combinational devices, constructed according to the second principle, is itself a combinational device as defined by the first. You may assume for the following that every input and output is a logical 0 or 1. Consider the following 2-input acyclic circuit whose two components, A and B, are each combinational devices:

\includepic{0.5}{Q1.png}

The propagation delay - the upper bound on the output settling time - for each device is specified in nanoseconds. The functional specifications for each component are given as truth tables detailing output values for each combination of inputs:

\begin{table}[h] \centering \begin{tabular}{c c|c c c c | c}  a_0a0​  &  a_1a1​  &  A _{a_0, a_1}Aa0​,a1​​  & \hspace{2cm} &  b_0b0​  &.  b_1b1​  &  B_{b_0. b_1}Bb0​.b1​​  \\ \hline 0 & 0 & 1 & & 0 & 0 & 0\ 0 & 1 & 0 & & 0 & 1 & 0\ 1 & 0 & 0 & & 1 & 0 & 0\ 1 & 1 & 1 & & 1 & 1 & 1\ \hline \end{tabular} \caption{} \end{table}

Answer the following questions,

1.  Give a truth table for the acyclic circuit, i.e. a table that specifies the value of z for each of the possible combinations of input values on x and y.

\ifanswers \beginsol

\begin{table}[h] \centering \begin{tabular}{c c | c} x & y & z \\ \hline 0 & 0 & 0 \\ 0 & 1 & 0 \\ 1 & 0 & 0 \\ 1 & 1 & 1 \\ \hline \end{tabular} \caption{} \end{table} \fi

1.  Describe a general procedure by which a truth table can be computed for each output of an arbitrary acyclic circuit containing only combinational components. \textit{Hint : construct a functional specification to each circuit node}. \ifanswers \beginsol We can construct the truth table from left to right, i.e: solve the truth table for each component from the leftmost all the way to the rightmost one by one. \fi
    
2.  Specify a propagation delay (the upper bound required for each combinational device) for the circuit.
    

\ifanswers \beginsol The total propagation delay is  3 + 2 = 53+2=5.

\fi

1.  Describe a general procedure by which a propagation delay can be computed for an arbitrary acyclic circuit containing only combinational components. \textit{Hint: add a timing specification to each circuit node}.

\ifanswers \beginsol One has to find the longest path from input to output to find the total propagation delay of the combinational circuit. \fi

1.  Do your general procedures for computing functional specifications and propagation delays work if the restriction to acyclic circuits is relaxed? Explain.

\ifanswers \beginsol No, the signal can propagate back in the circuit so using the longest path to calculate  t_{pd}tpd​  is not accurate. \fi

\newpage

### CMOS Circuit Boolean Expression

\includepic{0.5}{Q9}{} Draw the truth table of the CMOS circuit above. What is the boolean expression for the CMOS circuit shown?

\ifanswers \beginsol  F = \overline{A(B+C)D}F=A(B+C)D​

\begin{table}[h] \centering \begin{tabular} {c|c|c|c|c} A & B & C & D & F \\ \hline 0 & 0 & 0 & 0 & 1 \\ 0 & 0 & 0 & 1 & 1 \\ 0 & 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 1 & 1 \\ 0 & 1 & 0 & 0 & 1 \\ 0 & 1 & 0 & 1 & 0 \\ 0 & 1 & 1 & 0 & 0 \\ 0 & 1 & 1 & 1 & 0 \\ 1 & 0 & 0 & 0 & 1 \\ 1 & 0 & 0 & 1 & 1 \\ 1 & 0 & 1 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 \\ 1 & 1 & 0 & 0 & 1 \\ 1 & 1 & 0 & 1 & 0 \\ 1 & 1 & 1 & 0 & 1 \\ 1 & 1 & 1 & 1 & 0 \\ \hline \end{tabular} \caption{} \end{table}

\fi
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAyNTM2NDU4NF19
-->