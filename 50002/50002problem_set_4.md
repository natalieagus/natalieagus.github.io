---
layout: default
title: "Problem Set Week 4"
permalink: /50002/PS4/
---
50.002 Computational Structures 

Information Systems Technology and Design 

Singapore University of Technology and Design 

**Natalie Agus (Fall 2020)**

This page contains all practice questions that constitutes the topics learned in <ins>Week 4</ins>: **Programmability** and **Turing Machine**. 

Each topic's questions are grouped into **three** categories: basic, intermediate, and challenging. You are recommended to do all basic problem set before advancing further. 

{::options parse_block_html="true" /}
{% include toc.html %}
{::options parse_block_html="false" /}



### FSM Possibility (Basic)

  

We saw that certain functions, such as parentheses checking, cannot be performed by any finite state machine. **Which of the following can be performed by an FSM?** 

Assume, in each case, that the device is to take a series of `0`s and `1`s that represent the digits of a binary number entered *left-to-right*. 

1. The device is to have a **single** output, which is 1 only under this specific condition: *when the last 277 digits entered have been alternate `1`s and `0`s.*
	
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	**Yes**. It is a bit tedious for 277 digits, but you should be able to sketch FSM for 3 or 4 digits.
	</details>
	<br/>
	{::options parse_block_html="false" /}


1. The device is to have a **single** output, which is 1 only under this specific condition: *when more 0s than 1s have been entered*.


	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	**No**. Requires unbounded counting.
	</details>
	<br/>
	{::options parse_block_html="false" /}

1. The device is to have a **single** output, which is 1 only under this specific condition: *when the number entered thus far is **divisible** by 3.*


	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	**Yes**, can be done by a 3-state machine.
	</details>
	<br/>
	{::options parse_block_html="false" /}


1. The device is to have a **single** output, which is 1 only under this specific condition: *when an odd number of 1s and and even number of 0s have been entered.*


	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	**Yes**, can be done with a 4-state machine. 
	</details>
	<br/>
	{::options parse_block_html="false" /}

  

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

Unfortunately, the Universal FSM will have some fixed number (N) of states built into its design. So it won't have enough states to emulate machines with more than N states. Ben's idea isn't

workable.
</details>
<br/>
{::options parse_block_html="false" /}





\fi

  
  
  

### CPU

  
  
  

1. What are the four most important components of the von Neumann machine?

Draw their correlations.

\ifanswers

\beginsol

CPU, Memory, Device, and Bus. The connection is that the CPU, Memory, and Device are interconnected by the bus.

\fi

1. What are the four most important components of a CPU?

\ifanswers

\beginsol

This is the $\beta$ architecture: PC, Registers, Control Unit, and ALU

\fi

1. How much memory can a 32-bit von Neumann machine have? Why?

\ifanswers

\beginsol

$2^{32}$ because each address is 32 bits long (A word).

\fi

1. Can a CPU have as many registers as possible, in theory?

\ifanswers

\beginsol

No. The registers must be encoded in instructions, i.e: 5 bits for 32 registers. An instruction is 32 bits long for $\beta$ architecture, so having too many registers will make encoding infeasible.

\fi
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyODA4NDA0NzAsNTEwOTg0MDVdfQ==
-->