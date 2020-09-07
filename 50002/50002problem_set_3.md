---
layout: default
title: "Problem Set Week 3"
permalink: /50002/PS3/
---
50.002 Computational Structures 

Information Systems Technology and Design 

Singapore University of Technology and Design 

**Natalie Agus (Fall 2020)**


This page contains all practice questions that constitutes the topics learned in <ins>Week 3</ins>: **Sequential Logic and Synchronization** and **FSM*. 

Each topic's questions are grouped into **three** categories: basic, intermediate, and challenging. You are recommended to do all basic problem set before advancing further. 



{::options parse_block_html="true" /}
{% include toc.html %}
{::options parse_block_html="false" /}


# Sequential Logic and Synchronization

You can refer to the notes <a href="https://natalieagus.github.io/50002/sequential_logic" target="_blank">here</a> if you need to revise. 

### Warm-up Timing Computations (Basic)
  

Consider the following diagram of a simple sequential circuit:

<img src="https://www.dropbox.com/s/63cip82ur4u3y64/Q1.png?raw=1"  alt=“F1”  width="80%" height = "80%">
  
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

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU0MDU3ODg1NCwtNjEwNDczMDE4XX0=
-->