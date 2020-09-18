---
layout: default
title: "Problem Set Week 5"
permalink: /50002/PS5/
---
50.002 Computational Structures 

Information Systems Technology and Design 

Singapore University of Technology and Design 

**Natalie Agus (Fall 2020)**

This page contains all practice questions that constitutes the topics learned in <ins>Week 5</ins>:  **Beta Datapath**.

Each topic's questions are grouped into **three** categories: basic, intermediate, and challenging. You are recommended to do all basic problem set before advancing further. 

{::options parse_block_html="true" /}
{% include toc.html %}
{::options parse_block_html="false" /}

# Beta Datapath

### $\beta$ Assembly Language (Basic)

  

What does the following piece of Beta assembly do? Hand assemble the beta **assembly language** into **machine language**. 
  
```
I = 0x5678
B = 0x1234

LD(I,R0) -- (1)
SHLC(R0,2,R0) --  (2)
LD(R0,B,R1) -- (3)
MULC(R1,17,R1) -- (4)
ST(R1,B,R0)  -- (5)
```
Finally, **what is the result stored in R0?**


{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>


The machine language is:

```
I = 0x5678
B = 0x1234

|| LD(R31,I,R0) -> 011000 00000 11111 0101 0110 0111 1000 
0x601F5678
|| SHLC(R0,2,R0) -> 111100 00000 00000 0000 0000 0000 0010 
0xF0000002
||LD(R0,B,R1) -> 011000 00001 00000 0001 0010 0011 0100
0x60201234
||MULC(R1,17,R1) -> 110010 00001 00001 0000 0000 0001 0001
0xC8210011
||ST(R1,B,R0) -> 011001 00001 00000 0001 0010 0011 0100
0x64201234
```

Explanation:
1.  *Line 1:* move the content of the memory unit at `EA=I` to register `R0`

1.  *Line 2 :* the content of `R0` is multiplied by 4 and stored back at register `R0`

1.  *Line 3 :* move the content of memory address `EA`:  `EA` = `B` + content of register `R0`; to register `R1`

1.  *Line 4 :* The content of register `R1` is multiplied by 17 and stored back at register `R1`

1.  *Line 5 :* Store / copy the content of register R1 to the memory unit with address `EA`: `EA`= `B` + content of register `R0`.

The result of `R0` is the content of memory address I: `Mem[I]` multiplied by 4.
</details>
<br/>
{::options parse_block_html="false" /}

### Non $\beta$ Architecture Benchmarking (Basic)


A local junk yard offers older CPUs with non-Beta architecture that require **several clocks** to execute each instruction. Here are the specifications:
$$\begin{matrix}
\text{Model} & \text{Clock Rate} &  \text{Avg. clocks per Instruction}\\
\hline
x & 40 Mhz & 2.0\\
y & 100 Mhz & 10.0\\
z & 60 Mhz & 3.0\\
\end{matrix}$$

You are going to choose the machine which will execute your benchmark program the fastest, so you compiled and ran the benchmark on the three machines and counted the total instructions executed:

1.  $x$: `3,600,000` instructions executed

1.  $y$: `1,900,000` instructions executed

1. $z$: `4,200,000` instructions executed
  

Based on the above data, **which machine would you choose?**


{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>


First we find out the time taken to execute those instructions:

1.  $x$: $\frac{3.6M}{40M / 2}$ = $0.18$ seconds

1.  $y$: $\frac{1.9M} {100M / 10}$ = $0.19$ seconds

1. $z$: $\frac{4.2M}{60M / 3}$ = $0.21$ seconds

From the result above, $x$ is the fastest machine. Hence we choose $x$.
</details>
<br/>
{::options parse_block_html="false" /}
  


### Clumsy Lab Assistant (Basic)
Notta Kalew, a somewhat fumble-fingered lab assistant, has deleted the opcode field from the following table describing the control logic of an unpipelined Beta processor.

<img src="https://www.dropbox.com/s/hr0j3m2pmgbhvot/Q1.png?raw=1" width="70%" height="70%">

  

1.  Help Notta out by identifying which Beta instruction is implemented by each row of the table.

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	From first row to the last: `SUBC, BEQ, LDR, CMPEQ, ST`.
	</details>
	<br/>
	{::options parse_block_html="false" /}

2. Notta notices that `WASEL` is always zero in this table. Explain briefly under what circumstances `WASEL` would be non-zero.

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	`WASEL` is 1 if an *interrupt*, an *illegal* opcode is trapped, or a *fault* occurs. When `WASEL` is `1`, it selects `XP` as the write address for the register file; `Reg[XP]` is where we store the current `PC+4` whenever there is an interrupt, a fault, or an illegal opcode.
	</details>
	<br/>
	{::options parse_block_html="false" /}

3. Notta has noticed the following C code fragment appears frequently in the benchmarks:
	
	```
	int *_p; /_* Pointer to integer array *_/_
	_int i,j; /_* integer variables *_/_

	_..._

	_j = p[i]; /_* access ith element of array */
	```

	The pointer variable `p` contains the *address* of a **dynamically allocated** array of integers. The value of `p[i]` is stored at the address `Mem[p +4i]` where `p` and `i` are locations containing the values of the corresponding C variables. On a conventional Beta this code fragment is translated to the following instruction sequence:

	```
	LD(...,R1)     /* R1 contains p, the array base address */
	LD(...,R2)     /* R2 contains I, the array index */    ...
	SHLC(R2,2,R0)  /* compute byte-addressed offset = 4*i */
	ADD(R1,R0,R0)  /* address of indexed element */
	LD(R0,0,R3)    /* fetch p[i] into R3 */
	```

	Notta proposes the addition of an `LDX` instruction that shortens the last three instructions to:

	```
	SHLC(R2,2,R0)  /* compute byte-addressed offset = 4*i */
	LDX(R0,R1,R3)  /* fetch p[i] into R3 */
	```
	
	Give a ***register-transfer language description*** for the `LDX` instruction. 

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	```
	LDX( Ra, Rb, Rc )
	EA <- Reg[Ra] + Reg[Rb]
	Reg[Rc] <- Mem[EA]
	PC <- PC + 4
	```
	</details>
	<br/>
	{::options parse_block_html="false" /}

4. Using a table like the one above specify the control signals for the LDX opcode.

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	$$\begin{matrix}
	PCSEL & RA2SEL & ASEL & BSEL& WDSEL & ALUFN & WR & WERF & WASEL \\
	\hline
	0 & 0 & 0 & 0 & 2 & ADD & 0 & 1 & 0 \end{matrix}$$
	</details>
	<br/>
	{::options parse_block_html="false" /}

5. It occurs to Notta that adding an `STX` instruction would probably be useful too. Using this new instruction, `p[i] = j` might compile into the following instruction sequence:

```
SHLC(R2,2,R0)  /* compute byte-addressed offset = 4*i */
STX(R3,R0,R1)  /* R3 contains j, R1 contains p */
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjI2MDM3MjEzLC0xMTIwNDM5Nzg1XX0=
-->