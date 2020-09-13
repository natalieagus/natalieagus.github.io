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

### Synchronizability (Basic)
Which of the following cannot be made to function with perfect reliability, assuming reliable components and connections? **Explain your reasoning.** 

Some of the specifications refer to "bounded time" which means there is a *specified time interval*, measured from the most recent input transition, after which the output is stable and valid.

1. A circuit that in unbounded time indicates which of two game show contestants pressed their button first.
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	It is possible to build this *unbounded*-time arbiter. It may take an arbitrary period, after which it will produce:
	* A decision and
	* A signal that indicates that its made a decision.
	</details>
	<br/>
	{::options parse_block_html="false" /}
	
2. A circuit that in bounded time indicates which of two game show contestants pressed their button first.






# State Machine

You can refer to the notes <a href="https://natalieagus.github.io/50002/finite_state_machine.html" target="_blank">here</a> if you need to revise. 

### An Incomplete State Machine (Basic)
The ACME Company has recently received an order from a Mr. Wiley E. Coyote for their all-digital Perfectly Perplexing Padlock:
* The P3 has **two** buttons ("0" and "1") that when pressed cause the FSM controlling the lock to advance to a new state. 
* In addition to advancing the FSM, each button press is encoded on the B signal (B=0 for button "0", B=1 for button "1"). 
* The padlock **unlocks** when the FSM sets the UNLOCK output signal to 1, which it does whenever the last N button presses correspond to the unique N-digit combination.

  
Unfortunately the design notes for the P3 are *incomplete*. Using the specification above and clues gleaned from the partially completed diagrams below f**ill in the information that is missing from the state transition diagram** with its **accompanying truth table**. 

<img src="https://www.dropbox.com/s/1ww80s7vpxznf1k/Q1%202.png?raw=1" width="70%" height="70%">

When done,
*  Each state in the transition diagram should be assigned a 2-bit state name S1S0 (note that in this design the state name is not derived from the combination that opens the lock),

*  The arcs leaving each state should be mutually exclusive and collectively exhaustive,

*  The value for UNLOCK should be specified for each state, and o the truth table should be completed.

Also, **what is the combination of the lock**? 


{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

This state machine is a **Moore machine**. The completed state transition diagram and truth table is as follows:

<img src="https://www.dropbox.com/s/nstfdu7qea4dozo/Q2%202.png?raw=1" width="70%" height="70%">

The combination for the lock is `100`.
</details>
<br/>
{::options parse_block_html="false" /}

### Constructing an FSM (Basic)

Construct a "divisible-by-3" FSM that accepts a binary number entered one bit at a time, most significant bit first, and indicates with a *light* if the number entered so far is divisible by 3. Answer the following questions:

1.  Draw a state transition diagram for your FSM indicating the initial state and for which states the light should be turned on. *Hint: the FSM has 3 states.*
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	If the value of the number entered so far is N, then if digit b is entered next, the value of the new number N' is 2N + b. Using this fact:

	1.  If N is 0 mod 3 then for some p, N = 3p + 0. After the digit b is entered, N' = 6p + b. So N' is b mod 3.

	1.  If N is 1 mod 3 then for some p, N = 3p + 1. After the digit b is entered, N' = 6p + 2 + b. So N' is b+2 mod 3.

	1.  If N is 2 mod 3 then for some p, N = 3p + 2. After the digit b is entered, N' = 6p + 4 + b. So N' is b+1 mod 3.

	This leads to the following transition diagram where each state corresponds to each of the possible values of N mod 3.

	<img src="https://www.dropbox.com/s/kp3njg0hbw6kwwb/FSMqn.png?raw=1" width="70%" height="70%">

	</details>
	<br/>
	{::options parse_block_html="false" /}

2. Construct a truth table for the FSM logic. Inputs include the state bits and the next bit of the number; outputs include the next state bits and the control for the light.
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	$$
	\begin{matrix}
	S_1 & S_0 & b & S_1' & S_0' & \text{light} \\
	\hline 
	 0 & 0 & 0 & 0 & 0 & 1 \\
	 0 & 0 & 1 & 0 & 1 & 1 \\
	 0 & 1 & 0 & 1 & 0 & 0 \\
	 0 & 1 & 1 & 0 & 0 & 0 \\
	 1 & 0 & 0 & 0 & 1 & 0 \\
	 1 & 0 & 1 & 1 & 0 & 0 \\
	\hline
	\end{matrix}
	$$
	</details>
	<br/>
	{::options parse_block_html="false" /}

3. Write down the boolean equation for the FSM.
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	$$
	\begin{aligned}
	\text{light } &= \overline{S_1} * \overline{S_0}\\
	S_1' &= \overline{S_1} * S_0 * \overline{b} + S_1 * \overline{S_0} * b \\\\
	S_0' &= \overline{S_1} * \overline{S_0} * b + S_1 * \overline{S_0} * \overline{b}
	\end{aligned}
	$$
	</details>
	<br/>
	{::options parse_block_html="false" /}

### Hardware Implementation of a state machine (Intermediate)

Consider the schematic of a machine as follows, which function is to: *detect a sequence of three or more consecutive 1’s, and output: 1 after three or more consecutive 1’s, or 0 otherwise.*

<img src="https://www.dropbox.com/s/nx1s0kw3iu0cvqz/Q6.png?raw=1" width="70%" height="70%">

Let's analyse the circuit by answering the questions below:
1. If the circuit has an **initial** state of `AB=00`, and the input at `t=0` is `x=0`, what will the immediate next state be?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The immediate next state is: `AB = 00`. You can easily trace this output from the circuit above. 
	</details>
	<br/>
	{::options parse_block_html="false" /}

2. If the circuit has an **initial** state of `AB=00`, and the input at `t=0` is `x=1`, what will the immediate next state be?	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The immediate next state is: `AB = 01`
	</details>
	<br/>
	{::options parse_block_html="false" /}

3. If the circuit has a **current** state `AB=01`, and the current input is  `x=1`, what will the immediate next state be?	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The immediate next state is: `AB = 10`
	</details>
	<br/>
	{::options parse_block_html="false" /}

4. If the circuit has a **current** state `AB=11`, and the current input is  `x=1`, what will the immediate next state be?	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The immediate next state is: `AB = 11`
	</details>
	<br/>
	{::options parse_block_html="false" /}

5. If the circuit has a **current** state `AB=11`, and the current input is  `x=0`, what will the immediate next state be?	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The immediate next state is: `AB = 00`
	</details>
	<br/>
	{::options parse_block_html="false" /}

6. What are the state(s) that can go to state `AB=00` as its ***next*** state?
{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	All combinations: `AB=00`, or `01`, or `10`, or `11`. You can prove it easily by brute force: checking if `AB = 00` next if its previously set to some value `AB = ij` given existing value `x`.
	</details>
	<br/>
	{::options parse_block_html="false" /}

7. What is the value of output `y` when the current state is `AB = 11` and the current input is `x = 0`?
{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	Tracing it out, we have `y=1`. 
	</details>
	<br/>
	{::options parse_block_html="false" /}

8. The propagation delays for all the combinational logic gates and the flip-flops are `2ns`. The clock frequency is `100MHz`. **What is the worst case delay** in nanosecond for the next states at `A` and `B` to appear (i.e. for `A` and `B` to be valid) after the input `x` is changed to be a valid input. *Assume that the initial states `AB` are given and fixed.*
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	From the frequency, we can compute the *period* of the clock to be `10ns`. 

	For the **worst** case delay, we need to consider the scenario that input `x` is propagated up to input of the register and *it just missed the `clk` rise*. It takes `4ns` to propagate through the `AND` and `OR` gates, and another `10ns` to wait for another `clk` rise. Finally, it takes `2ns` to propagate through the register to produce `A` or `B`. Hence the **worst case delay** is `4+10+2 = 16ns`.
	</details>
	<br/>
	{::options parse_block_html="false" /}


9. The **propagation** delays for all the combinational logic gates and the flip-flops are `2ns`. Each `dff` have $t_H$ and $t_S$ of `1ns` each.  If the clock frequency is not given, what is the **maximum clock frequency** *(smallest `clk` period)* that we can have for this device?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The clock period has to satisfy the *feedback* path ($t_2$ timing constraint), that is made up with $t_{PD}$ of the `dff`,  $t_{PD}$ of the `AND` gate,  $t_{PD}$ of the `OR` gate, plus $t_S$ of the register. This adds up to `2+2+2+ 1 = 9ns`. Hence the maximum frequency is $\frac{1}{(9*10^{-9})}$ `= 111111111.11Hz = 111.11MHz`.
	</details>
	<br/>
	{::options parse_block_html="false" /} 

10. What are the output sequences from `t=1` to `t=16` of the circuit when fed the following input (fed from *left* to *right*): `1101 1111 1110 0010` from `t=0` to `t=15` respectively? Assume that the initial states are `AB=00`.
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	Given that the initial state is `AB=00`, that makes `B' = 1` at `t=0`.  This is doable the tedious way by simply tracing the output `y` sixteen times from `t=1` to `t=16`. We can also deduce from the *functionality* of the device, that is to **detect** three consecutive `1`'s and output `0` afterwards. The output sequence is therefore `0000 0010 0000 0000` from `t=1` to `t=16` repectively.
	</details>
	<br/>
	{::options parse_block_html="false" /}

### State-Machine Timing Computation (Intermediate)

Take a look at the following State Machine circuitry:

<img src="https://www.dropbox.com/s/d8o2nhv1ugouf2g/Q3.png?raw=1" width="70%" height="70%">

The device `A2` has the following schematic:
<img src="https://www.dropbox.com/s/9e2jzfrwtjto34p/Q4.png?raw=1" width="40%" height="40%">


It is made out of this device we call `A000R` with $t_{CD}$ = `1ns`, and $t_{PD}$ = `3ns` with the following schematic
<img src="https://www.dropbox.com/s/55rj88ehoozyo6y/Q5.png?raw=1" width="40%" height="40%">

The truth table for `A000R` is as follows: 
$$
\begin{matrix}
    A & B & C & D & E \\
    \hline 
    0 & 0 & 0 & 0 & 0 \\
    0 & 0 & 1 & 1 & 0 \\
    0 & 1 & 0 & 1 & 0 \\
    0 & 1 & 1 & 0 & 1 \\
    1 & 0 & 0 & 1 & 0 \\
    1 & 0 & 1 & 0 & 1 \\
    1 & 1 & 0 & 0 & 1 \\
    1 & 1 & 1 & 1 & 1 \\
    \hline
\end{matrix}
$$

The timing specifications for other devices in the state machine is:
*  The Mux has the following time specification: $t_{CD}$ = `1ns`, and $t_{PD}$ = `2ns`.

* The Registers has the following time specification: $t_{CD}$ = `2ns`, $t_{PD}$ = `5ns`, $t_S$ = `2ns`, $t_H$ = `2ns`.

Both `A1` and `A2` are **combinational** logic that contains `A000R` only. Unfortunately, the design for `A1` is *missing*. We only know that `A1` uses only `A000R` to compute the output and the next state function **and that A1 has the same $t_{PD}$ as A2**. The other information that we have is that the output of `A1`, `X[2:0]` is a sequence of decimal, `[1, 2, 3, ... ]` in the *binary* form, i.e. `[001, 010, 011, ...]`.

Answer the following questions:
1. How many bits should the constant `Z1` have?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	Since one of the inputs to the muxes are 3-bits, this hardware is implemented using three 2-input mux. `Z1` is essentially **three bits**, connected to *each* of the three copies of 2-input muxes.
	</details>
	<br/>
	{::options parse_block_html="false" /}

2. How many bits should the constant `Z2` have?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	**1 bit**. The number of bits of each input to a combinational logic device such as A1 *does not depend on anything else or other inputs.*
	</details>
	<br/>
	{::options parse_block_html="false" /}

3. What is the decimal value of `Z1`?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	Since `X[2:0]` produces an increasing sequence from decimal value of `1,2,3,4,...` etc, we can easily guess that the the decimal value of `Z1` should be `0`, such that when there's a `RESET`, the output of the register `R1` is zero.
	</details>
	<br/>
	{::options parse_block_html="false" /}

4. What is the decimal value of `Z2`?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	`Z2`'s decimal value is `1`. The same reason applies: since the sequence `X[2:0]` produced by `A1` is increasing by 1, the input to `A1` should be 1 such that at *every* cycle, theres an addition of 1 to be produced at `X`.
	</details>
	<br/>
	{::options parse_block_html="false" /}

5. What is the $t_{PD}$ of `A2` in nanosecond?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The  $t_{PD}$  of `A000R` is 3ns, hence the  $t_{PD}$  of `A2` is `9ns` since it is made out of three `A000R` modules connected in series.
	</details>
	<br/>
	{::options parse_block_html="false" /}

6. What is the minimum clock period in nanosecond?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The *longest* path that the clock period has to satisfy is `R1 -> A1 -> A2 -> Z1 -> R2`. Hence we need to consider the $t_{PD}$ of all devices in its path (except `R2`) plus $t_S$ of `R2`: `5+9+9+2+2 = 27ns`.
	</details>
	<br/>
	{::options parse_block_html="false" /}


7. What is the minimum $t_{CD}$ of `A1` in nanosecond?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	$t_{CD}$ of `A1` has to be large enough so as to satisfy  $t_H$ of `R1`. $t_H$ of `R1` is `2ns`, and  $t_{CD}$ of the mux is `1ns`. Therefore min $t_{CD}$ of `A1` is `2-1 = 1ns`.
	</details>
	<br/>
	{::options parse_block_html="false" /}

8. What is value of `A2`'s $t_{CD}$ in nanosecond?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The $t_{CD}$ of `A2` is basically the $t_{CD}$ of a single `A000R` (`1ns`) since that is the *shortest* path from any input to any output in `A2`.
	</details>
	<br/>
	{::options parse_block_html="false" /}

9. When `RESET` is `1` for several cycles, what will be the value of `X[2:0]`?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	When `RESET` is `1`, the output of `R1` will be `000`. Hence the value of `X[2:0]` will be `001`.
	</details>
	<br/>
	{::options parse_block_html="false" /}

10. When X's output is sequences of value `[1, 2, 3, ...]`, what is the value of `RESET`?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	`RESET` has to be `0` to enable the *addition* of the previous value of X to take effect, and form a new value of X in the next clock cycle.
	</details>
	<br/>
	{::options parse_block_html="false" /}

Now, suppose that at time `t=0`, `RESET` signal is changed from `1` to `0`, and `X` becomes `001`. From then on, `RESET` remains 0:

1. What is the decimal value of `O[2:0]` at time `t = 0`?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	`X` is `001`  and `Y` is `000`  at `t=0`. Using the truth table of `A000R` and the schematic of `A1`, we can deduce that `O[2:0]` at `t=0` is `1`.
	</details>
	<br/>
	{::options parse_block_html="false" /}

2. What is the decimal value of `O[2:0]` at time `t = 1`?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	X is `010` and Y is `001` at `t=1`. Using the truth table of `A000R` and the schematic of `A1`, we can deduce that `O[2:0]` at `t=1` is `3`.
	</details>
	<br/>
	{::options parse_block_html="false" /}

3. What is the decimal value of `O[2:0]` at time `t=3`?
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	X is `011` and Y is `011` at `t=1`. Using the truth table of `A000R` and the schematic of `A1`, we can deduce that `O[2:0]` at `t=2` is `2`.
	</details>
	<br/>
	{::options parse_block_html="false" /}









 





<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU2NzAyMjI1NywyMTE1Njk0OTY1LDEwNj
czNjEwMzgsMTA3MjQ1NjM1MSwzNzYwNzg2NjAsLTE2NjczMjA3
NjEsLTE5NTczNzU5NDQsLTk3MTMyOTk5NywtMTkyODQ0MDgyNi
wtNjEwNDczMDE4XX0=
-->