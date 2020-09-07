---
layout: default
title: "Problem Set Week 3"
permalink: /50002/PS3/
---
50.002 Computational Structures 

Information Systems Technology and Design 

Singapore University of Technology and Design 

**Natalie Agus (Fall 2020)**


This page contains all practice questions that constitutes the topics learned in <ins>Week 3</ins>: **Sequential Logic and Synchronization** and **FSM**. 

Each topic's questions are grouped into **three** categories: basic, intermediate, and challenging. You are recommended to do all basic problem set before advancing further. 



{::options parse_block_html="true" /}
{% include toc.html %}
{::options parse_block_html="false" /}


# Sequential Logic and Synchronization

You can refer to the notes <a href="https://natalieagus.github.io/50002/sequential_logic" target="_blank">here</a> if you need to revise. 

### Warm-up Timing Computations (Basic)
  

Consider the following diagram of a simple sequential circuit:
<img src="https://www.dropbox.com/s/63cip82ur4u3y64/Q1.png?raw=1" width="70%" height="70%">
  
The components labeled CL1 and CL2 are combinational; R1 and R2 are edge triggered flip flops. Timing parameters for each component are as noted. Answer both questions below:

1. Write the timing specifications (tS, tH, tCD, tPD, tCLK) for the system as a whole using the timing specifications for the internal components that are given in the figure.

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	$t_H$ and $t_S$ is for IN, $t_{CD}$ and $t_{PD}$ is for CLK. Below are the proposed values:
	$$
	\begin{aligned}
	t_S &= t_{S.R1} + t_{PD.CL1} = 3 + 3 = 6\\
	t_H &= t_{H.R1} - t_{CD.CL1} = 2 - 1 = 1\\
	t_{CD} &= t_{CD.R2} = 2\\
	t_{PD} &= t_{PD.R2} = 8\\
	t_{CLK} &\geq t_{PD.R1} + t_{PD.CL2} + t_{S.R2} = 2 + 5 + 4 = 11
	\end{aligned}$$
	</details>
	<br/>
	{::options parse_block_html="false" /}
	
3. Suppose you had available a faster version of CL2 having a propagation delay of 3 and a contamination delay of zero. Could you substitute the faster CL2 for the one shown in the diagram **Explain.**

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>
	
	No we can't. The contamination delay for R1 is 1, while the contamination delay for CL2 is 0. After CLK change, R2 input holds for 1s, but $t_H$ required is 2s.
	</details>
	<br/>
	{::options parse_block_html="false" /}

### Timing Plot Analysis (Basic)
Consider the following unusual D-latch configuration:
<img src="https://www.dropbox.com/s/vxvoeomb1zyc7h0/Q7.png?raw=1" width="70%" height="70%">
 
Now we feed it the following input signal and CLK signal. **Which of the following signal plots represent the output of this device made out of 3 D-latches?** Assume that the jagged edges means unknown value and that the contents of each latch in the beginning is unknown.
<img src="https://www.dropbox.com/s/7a8ww9nvk0lzlfq/Q7b.png?raw=1" width="70%" height="70%">

{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

**SIGNAL 2** is the output of the device since there's two *unknown* outputs (it takes two half-clock cycles for the input to be propagated to the output). 

Signal 5, although it has "invalid" values for two clock cycles isn't the answer because since it is an odd-numbered DFFs, it will  **change output** at the **falling** edge, as opposed to rising edge in a normal DFF with two latches.
</details>
<br/>
{::options parse_block_html="false" /}


### Another Timing Computations (Basic)

Consider the following circuit, and notice the **feedback loop**:

<img src="https://www.dropbox.com/s/jhq2pg9rs70rlrj/Q8.png?raw=1" width="70%" height="70%">

Setup time, hold time, propagation delay, and contamination delay (all in nanoseconds) of each component is as written above. Lets now analyse its timing constraints:

1.  What is the minimum contamination delay (tcd) of Combinational Logic 1 such that the sequential circuit may still function properly?


{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

The combinational logic unit 1 (CL1) is responsible for the hold times of R4 and R1. Since R1's tHold is larger than R4, we should consider that to compute min tcd for CL1. The thold of R1 can be satisfied using the tcd of CL1 plus the $\min tcd$ of either R1, R2, or R3. Hence, minimum acceptable tcd of CL1 is thold R1 - tcd R2 = 3 - 1 = 2ns.

\fi

1.  Write down the minimum CLK period for the sequential circuit to function properly.

\ifanswers

\beginsol

The clock period must be big enough for signals to propagate from the upstream registers on the left to any downstream registers R1 or R4. The longest path is formed by the tpd of R1 + tpd CL1 + tSetup R4 = 1 + 2 + 2 = 5ns.

\fi

1.  Write down the minimum hold time (tH) for the IN signal to the system.

\ifanswers

\beginsol

The input must satisfy the thold of both R2 and R3, which is 3ns.

\fi

1.  Write down the minimum propagation time of the sequential logic circuit.

\ifanswers

\beginsol

The propagation time of the circuit is counted from R4 onwards since it is the last register in the circuit, hence it tpd R4 + tpd CL2 = 3.1ns.

\fi

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyOTU1Njc2MDEsLTE5Mjg0NDA4MjYsLT
YxMDQ3MzAxOF19
-->