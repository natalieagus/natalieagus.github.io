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

You can refer to the notes <a href="https://natalieagus.github.io/50002/sequential_logic.html" target="_blank">here</a> if you need to revise. 

### Warm-up Timing Computations (Basic)
  

Consider the following diagram of a simple sequential circuit:
<img src="https://www.dropbox.com/s/63cip82ur4u3y64/Q1.png?raw=1" width="70%" height="70%">
  
The components labeled CL1 and CL2 are combinational; R1 and R2 are edge triggered flip flops. Timing parameters for each component are as noted. Answer both questions below:

1. Suggest the values for each timing specifications ($t_S$, $t_H$, $t_{CD}$, $t_{PD}$, $t_{CLK}$ -- clock period) for the system **as a whole** using the timing specifications of each of the internal components that are given in the figure. 

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

1.  What is the minimum contamination delay ($t_{CD}$) of Combinational Logic 1 such that the sequential circuit may still function properly?


	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The combinational logic unit 1 (CL1) is responsible for the hold times of R4 and R1. Since R1's $t_{H}$ is larger than R4, we should consider that to compute min $t_{CD}$ for CL1.  

	$t_{H}$ of R1 can be satisfied using the $t_{CD}$ of CL1 plus the $\min t_{CD}$ of either R1, R2, or R3. 

	Hence, minimum acceptable $t_{CD}$ of CL1 is $t_{H}$ R1 - $t_{CD}$ R2 = 3 - 1 = 2ns.
	</details>
	<br/>
	{::options parse_block_html="false" /}

1.  Write down the minimum CLK period for the sequential circuit to function properly.


	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The clock period must be big enough for signals to propagate from the upstream registers on the left to any downstream registers R1 or R4. The longest path is formed by the $t_{PD}$ of R1 + $t_{PD}$ CL1 + $t_{S}$ R4 = 1 + 2 + 2 = 5ns.
	</details>
	<br/>
	{::options parse_block_html="false" /}

1.  Write down the minimum hold time ($t_{H}$) for the IN signal to the system.


	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The input must satisfy the $t_{H}$ of both R2 and R3, which is 3ns.
	</details>
	<br/>
	{::options parse_block_html="false" /}

1.  Write down the minimum propagation time of the sequential logic circuit.


	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The propagation time of the circuit is counted from R4 onwards since it is the last register in the circuit, hence it $t_{PD}$ R4 + $t_{PD}$ CL2 = 3.1ns.
	</details>
	<br/>
	{::options parse_block_html="false" /}


### Metastable State Analysis (Basic)

Consider the following D-latch device and its VTC plot:
<img src="https://www.dropbox.com/s/ojcjpgj8g7da5oj/Q9.png?raw=1" width="70%" height="70%">
  

We are given the following specification about the multiplexer's valid operating voltage ranges: $V_{IL} = 1V, V_{OL} = 0.5V, V_{IH} = 3V, V_{OH} = 3.5V$. The noise margin is $0.5V$ and we can assume that the device obeys the **static discipline**.

1.  Which voltage value approximately, has the highest probability for the device to be in the metastable state?

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	We plot the line Vout == Vin and find the intersection with the VTC curve to be approximately at 2.35V. This is the Vin value that has the highest probability for the device to stay in metastable state.
	</details>
	<br/>
	{::options parse_block_html="false" /}

1.  Compare $V_{IN} = 0.9V$ vs $V_{IN} = 3V$. Which input voltage will most likely  cause the device stay in the metastable state?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	Both input voltage values are **valid** inputs. Therefore the device will **always produce valid output voltages** since it obeys the static discipline. We can say that both values are equally unlikely to stay in the metastable state.
	</details>
	<br/>
	{::options parse_block_html="false" /}

1.  Compare $V_{IN} = 2.1V$ vs $V_{IN} = 2.5V$. Which input voltage will most likely  cause the device stay in the metastable state?

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	Both input voltage values are *invalid* inputs. 

	From the graph, we can deduce that $V_{IN} = 2.1V$ results in $V_{OUT} = 1V$, while $V_{IN} = 2.5V$  results in $V_{OUT} = 3.3V$. 

	Taking $2.35V$ as the most likely voltage value for the device to stay in the metastable state, $3.3V$ is nearer to $2.35V$ as opposed to $1V$. Hence, we can deduce that  $V_{IN} = 2.5V$ is more likely to cause the device to stay in the metastable state.
	</details>
	<br/>
	{::options parse_block_html="false" /}

### Determining Suitable Clock Period (Intermediate)

The following circuit diagram implements a sequential circuit with two state bits, `S0` and `S1`:

<img src="https://www.dropbox.com/s/6tivnh73831oza5/Q2.png?raw=1" width="70%" height="70%">

Answer the following questions:

1.  What is the smallest clock period for which the circuit still operates correctly?

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	There are two contraints to check:

	$$\begin{aligned}
	t_{PD.REG} + t_{PD.INV} + t_{PD.INV} + t_{S.REG} & \leq t_{CLK}\\
	t_{PD.REG} + t_{PD.NOR2} + t_{S.REG} &\leq t_{CLK}
	\end{aligned}$$

	We need to find the largest value of $t_{CLK}$ that satisfies both constraints. This comes from the first constraint that requires $t_{CLK} \geq$ 9ns.
	</details>
	<br/>
	{::options parse_block_html="false" /}

1.  A sharp-eyed student suggests optimizing the circuit by removing the pair of inverters and connecting the Q output of the left register directly to the D input of the right register. If the clock period could be adjusted appropriately, would the optimized circuit operate correctly? If yes, explain the adjustment to the clock period will be needed. 

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	No, the circuit won't operate correctly since $t_{CD.REG} < t_{HOLD.REG}$, i.e., the output of the left register doesn't meet the required hold time when connected directly to the input of the right register.
	</details>
	<br/>
	{::options parse_block_html="false" /}

1.  When the RESET signal is set to "1" for several cycles, what values are `S0` and `S1` set to?


	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	`S0 = 0, S1 = 0`.
	</details>
	<br/>
	{::options parse_block_html="false" /}

1.  Assuming the RESET signal has been set to "0" and will stay that way, what is the state following S0=1 and S1=1?

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	`S0 = 1, S1 = 0`.
	</details>
	<br/>
	{::options parse_block_html="false" /}



# State Machine

You can refer to the notes <a href="https://natalieagus.github.io/50002/finite_state_machine.html" target="_blank">here</a> if you need to revise. 

### Hardware Implementation of a state machine (Intermediate)

Consider the schematic of a machine as follows, which function is to: *detect a sequence of three or more consecutive 1’s, and output: 1 after three or more consecutive 1’s, or 0 otherwise.*

<img src="https://www.dropbox.com/s/nx1s0kw3iu0cvqz/Q6.png?raw=1" width="70%" height="70%">

Let's analyse the circuit by answering the questions below:
1. If the circuit has an initial state of `AB=00`, and the input at `t=0` is `x=0`, what will the immediate next state be?
{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

The immediate next state is: `AB = 00`
</details>
<br/>
{::options parse_block_html="false" /}

2. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NjYxNTkzODYsLTE2NjczMjA3NjEsLT
E5NTczNzU5NDQsLTk3MTMyOTk5NywtMTkyODQ0MDgyNiwtNjEw
NDczMDE4XX0=
-->