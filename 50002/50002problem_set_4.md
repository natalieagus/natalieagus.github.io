---
layout: default
title: "Problem Set Week 4"
permalink: /50002/PS4/
---
50.002 Computational Structures 

Information Systems Technology and Design 

Singapore University of Technology and Design 

**Natalie Agus (Fall 2020)**

This page contains all practice questions that constitutes the topics learned in <ins>Week 4</ins>:  **Turing Machine** and **Programmability**. 

Each topic's questions are grouped into **three** categories: basic, intermediate, and challenging. You are recommended to do all basic problem set before advancing further. 

{::options parse_block_html="true" /}
{% include toc.html %}
{::options parse_block_html="false" /}



# Turing Machine

### Ben's Turing Machine (Basic)

  
Ben Bitdiddle's proposed Ph.D. thesis involves writing a program to compute a function $f(x)$ on a Cray supercomputer. Ben's advisor points out that $f$ cannot be computed on any Turing machine. **Should Ben care? Why?**

{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

Church's thesis says that if the function can't be computed on any Turing machine, then it can't be computed on any physically realizable machine that we know of. So Ben is out of luck... a Cray *supercomputer* isn't "super" in that sense.
</details>
<br/>
{::options parse_block_html="false" /}
  
  

Discouraged by your answer to the last question, Ben has turned his attention to an alternative thesis topic. **He now proposes to invent the universal FSM,** which will be to FSMs what a universal Turing machine is to Turing machines. Ben's idea is to build an FSM that can fed a sequence of inputs describing any other FSM and the inputs to that FSM. The universal FSM would then *emulate* the behavior of the described FSM on the specified inputs. **Is Ben's idea workable Why or why not?**


{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

Unfortunately, the Universal FSM will have some fixed number (N) of states built into its design. So it won't have enough states to emulate machines with more than N states. Ben's idea isn't workable, and there's no such thing as "Universal FSM" as he proposed.
</details>
<br/>
{::options parse_block_html="false" /}
  

### CPU Trivia (Basic)

1. How much memory can a 32-bit von Neumann machine have? *Explain your answer.*

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	$2^{32}$ **bytes** because each address is also 32 bits long in a 32-bit von Neumann machine.
	</details>
	<br/>
	{::options parse_block_html="false" /}


2. Can a CPU have as many registers as possible, in theory?


	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	**No**. *Addresses* for each register involved in the instruction must be encoded *within the instruction*, i.e: 5 bits for 32 registers. An instruction is 32 bits long for $\beta$ architecture, so having too many registers will make encoding infeasible.
	</details>
	<br/>
	{::options parse_block_html="false" /}


### Non $\beta$ Architecture Benchmarking


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
  

### Memory Addressing (Basic)

  
You are given that the 32-bit *word* at memory address `0` has a binary form of
```
0000 0100 0000 0011 0000 0010 0000 0001
```

What is the value of the *byte* stored in address `0, 1, 2` and `3`, respectively? What are the hexadecimal forms of the bytes?

{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

1, 2, 3, and 4 are stored at address `0, 1, 2, 3` respectively.  The hex form is the word: 0x04 03 02 01.
</details>
<br/>
{::options parse_block_html="false" /}

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzMzMTkyMDY0LC0yMTM5MzA0MzYxLC0yMT
M4MDI1MDU0LDUxMDk4NDA1XX0=
-->