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

### $\beta$ Trivia (Basic)
1.  In an unpipelined Beta implementation, when is the signal `RA2SEL` set to `1`?

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The `RA2SE`  signal is set to `1` when executing a `ST` instruction. When `RA2SEL` is `1` the 5-bit `Rc` field of the instruction is sent to the `RA2` port of the register file, causing `Reg[Rc]` to be sent to the **write data port of main memory.**
	</details>
	<br/>
	{::options parse_block_html="false" /}

2. In an unpipelined Beta implementation, when executing a `BR(foo,LP)` instruction to call procedure `foo`, what should `WDSEL` should be set to?

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	`BR(foo,LP)` is a *macro* for `BEQ(R31,foo,LP)`. All `BNE/BEQ` instructions save the address of the following instruction in the specified destination register (`LP` in the example instruction). So `WDSEL` should be set `0`, selecting the output of the `PC+4` logic as the data to be **written into the register file.**
	</details>
	<br/>
	{::options parse_block_html="false" /}

3. The **minimum clock period** of the unpipelined Beta implementation is determined by the *propagation* *delays* of the datapath elements and the amount of time it takes for the **control signals to become valid**. **Which** of the following select signals should become valid first in order to ensure the smallest possible clock period: `PCSEL, RA2SEL, ASEL, BSEL, WDSEL, WASEL`?
	
	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	To ensure the **smallest** possible clock period `RA2SEL` should become valid first. The `RA2SEL` mux must produce a **stable register address** before the register file can do its thing. All other control signals affect logic that operates **after** the required register values have been accessed, so they don't have to be valid until *later* in the cycle.
	</details>
	<br/>
	{::options parse_block_html="false" /}


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

	Briefly describe what (hardware) **modifications** to the Beta datapath would be necessary to be able to execute `STX` in a **single cycle.**

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	The register transfer language description of  `STX` would be:
	```
	STX(Rc, Rb, Ra)
	EA <- Reg[Ra] + Reg[Rb]
	Mem[EA] <- Reg[Rc]
	PC <- PC + 4
	```

	It's evident that we need to perform **3 register reads,** but the Beta's register file has only **2 read ports.** Thus we need to add a **third read port** to the register file.

	Incidentally, adding a third read port would eliminate the need for the `RA2SEL` mux because we *no longer need to choose between `Rb` and `Rc`*, since each register field has its own read port.
	</details>
	<br/>
	{::options parse_block_html="false" /}


### New Beta Instruction (Intermediate)
Write the register transfer language below corresponds to the instruction with the following control signal:
<img src="https://www.dropbox.com/s/ysf5rtc0d9mwsil/ctrlnew.png?raw=1" width="20%" height="20%">

{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

```
PC <-- PC + 4
Reg[Rc] <-- (PC+4)+4*SXT(C) 
```
</details>
<br/>
{::options parse_block_html="false" /}

### Another New Beta Instruction (Basic)
Given the following C-code:

```
if (a != 0){ 
	b = 3;
}  
(other code....)
```

where `a`, `b` are variables that have been initialised in the earlier part of the code (not shown). If we were to implement the following C-code using the Beta instruction set, we must do this in at least **two** cycles:

```
BEQ(Ra, label_continue, R31)  
ADDC(R31, 3, Rb)  
label_continue: (other code)
```

where `Ra`, `Rb` are assumed to be registers **containing** values `a` and `b`.

The `ALU` in this particular  Beta however, implements *five* new functions on top of the standard functions: `“B”, “NOTA”, “NOTB”, “TRUE”, “FALSE”`. 

Due to this, your classmate suggested that we can actually do this in **one** cycle by modifying the `Control Unit` to accept  this **new instruction** called `MCNZ` (move constant if not zero) instead:

```
MCNZ(Ra, literal, Rc) : 
	if(Reg[Ra] != 0)
		Reg[Rc] <-- literal 
	PC <-- PC + 4
```

What values should the Control Unit give for this instruction `MCNZ`?

{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

$$\begin{matrix}
	PCSEL & RA2SEL & ASEL & BSEL& WDSEL & ALUFN & WR & WERF & WASEL \\
	\hline
	0 & - & - & 1 & 1 & "B" & 0 & Z?0:1 & 0 \end{matrix}$$
Note: `Z?0:1` -- means `0` if `Z==1`, and `1` otherwise.
</details>
<br/>
{::options parse_block_html="false" /}


### Faulty Detection in Beta (Intermediate)

You suspected that your Beta CPU is faulty, in particular, these two components:
* The `ASEL` **mux** might be faulty: 
	* if `ASEL = 0`, the output is always 0. 
	* There's no problem if `ASEL = 1`.  
	
* The part of the `CU` that gives out `RA2SEL` signal might be faulty: 
	* `RA2SEL` is always **stuck at `0`** (it cannot be `1` regardless of the instruction)

Your friend came up with several short test programs. You want to select one of these programs to run in the faulty Beta, but you don't want to waste your time loading and running multiple programs and would like to select one that can **detect both faults**. Which of the following program(s) can detect **both faults?**

*Meaning that :*
1.  The values in the `PC` / Registers in Regfile / Memory Unit will be *different* from a working Beta CPU if these programs were to be executed in this faulty Beta. 
   
2.  You can be 100% sure the discrepancy is caused by **both** `RA2SEL` signal or `ASEL` mux faulty.
    
3.  Programs that can only detect the `RA2SEL` signal faulty but not `ASEL` multiplexer faulty (or vice versa) is **not acceptable**. 

*You can assume that the initial content of all registers are `0`.* 

**Program 1**:
```
.=0x000  
LDR(constant, R0) 
LDR(constant + 4, R1) 
ADD(R0, R1, R2)  
ST(R2, constant + 8, R31) 
HALT()  

constant: LONG(8)
LONG(4)
```

**Program 2**:
```
.=0X000  
CMOVE(5, R1) 
LDR(constant, R2) 
ST(R2, answer, R31) 
MUL(R1, R2, R3) 
HALT()  

constant: LONG(0) 
.=0xFFFC  
answer: LONG(0)
```

**Program 3**:
```
.=0x000  
constant: LONG(8)
LONG(4)
LDR(constant, R0) 
ADD(R0, R0, R0) 
ST(R0, .+8, R31) 
HALT()
```

**Program 4**:
```
.=0x000  
CMOVE(5, R0)  
ST(R0, constant + 8, R31) 
LDR(constant, R1)  
ADD(R1, R1, R2)  
HALT()  

.=0xABCC  
constant: LONG(8)
LONG(4)
```

{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>

There's only one instruction: `ST` that requires `RA2SEL` to be `1`. Therefore our program must have this instruction to test against a working Beta CPU. We also must ensure that we utilize instructions that results in `ASEL=0` and that the output of the `ASEL` mux should be nonzero in a working Beta CPU. We also need to ensure that the programs need to *utilize* these instructions in a way that results in a different **state** when run on a working Beta CPU.   

**Program 1** and **Program 4** fulfills the criteria, and the other two don't. 

For **Program 1**:
* The content store at `R2` will be 4 instead of 12 if the `ASEL` mux is faulty. 
* We will end up storing 8 instead of 12 to `Mem[constant + 8]` if `RA2SEL` signal remains `0` due to the faulty `CU`. 

For **Program 4**:
* The content of `R21` is stored to `Mem[Constant+8]` instead of the content of `R0`. Therefore, `Mem[Constant+8]`  is `0` instead of `5`. 
* The content of `R2` is 5 instead of 10. 

**Program 2** and **Program 3** also utilizes `ST` and `OP` instructions: `MUL`/`ADD`, etc that involve the `ASEL` mux but if you run them with the faulty Beta and with a working Beta, the end state is either the same or different due to one of the faulties only, and therefore can't be used to detect both faulties. 
</details>
<br/>
{::options parse_block_html="false" /}

### Beta Instruction Replacements (Intermediate)

For each of the statements below, indicate whether they're True or False and provide your reasoning. 

* **Statement 1:**  In the Beta, every `ADDC` instruction can **always** be replaced by a `SUBC` instruction that puts precisely the **same** value in the destination register. For example, `ADDC(R0,1,R0)` is equal to `SUBC(R0,-1,R0)` (*think about all constants*).  

* **Statement 2:** In a Beta program, you can use `BEQ(R31, label, R31)` as a substitute for `JMP(Ra)` where `Ra` stores the address of `label`, no matter where `label` is. 

* **Statement 3:** We can never perform `LD` and `ST`  to any two independent addresses in a *single cycle* (even if the memory unit supports it) by just modifying the **control unit** of the Beta. In other words, we need to modify the datapath of the Beta in order to do this. 

	{::options parse_block_html="true" /}
	<details>
	<summary markdown="span">Show Answer</summary>

	**Statement 1** is **False**. We can have `ADDC(R0, -65536, R0)` but we cant have `SUBC(R0, 65536, R0)` as the most positive number that a signed 16-bit can represent is `65535`. 

	**Statement 2** is **False**. `Ra` contains 32-bit of data, so we can set `PC` to be pointing to *any* address in the memory (4GB of address space) with `JMP(Ra)`. However, `BEQ` only covers `65536*4` *(above `PC+4`*) + `65535*4` (*below and inclusive of `PC+4`*) bytes of address space.

	**Statement 3** is **True**. The output of the `ALU` supplies a **single** address for both load and store to the memory unit. 

	</details>
	<br/>
	{::options parse_block_html="false" /}

### PCSEL Fault Detection (Intermediate)

This time round, consider a Beta machine with a faulty **control unit**, where its `PCSEL` signal is always `0`, meaning that the input to the `PC` register is always  
`PC+4` *regardless* of the instruction.

As always, we can  detect this particular fault by running a simple test program written in Beta assembly language. State which of the following programs can **detect** this particular fault, meaning that if it was to be run on a faulty Beta machine, we will get different results (contents) on the registers in the regfiles, PC, or Memory Unit, and provide your reasoning. 

Assume that all register values were `0` at the beginning of each program execution.

**Program 1**: (executed for two CLK cycles)
```
.= 0  
BEQ(R0, .+4, R31)  
ADDC(R0, 1, R0)  
```

**Program 2**: (executed for three CLK cycles)
```
.=0  
CMPEQ(R0, R0, R0)  
BNE(R0, .-4, R31)  
ADDC(R0, 1, R0)
```

**Program 3**: (executed for four CLK cycles)
```
.=0  
LD(R0, 0, R0)  
MULC(R0, 1, R0)  
BNE(R0, .+4, R31)  
CMPEQ(R0, R31, R2)
```

**Program 4**: (executed for two CLK cycles)
```
.=0
ST(R0, x, R31) 
x: LONG(12)
```

**Program 5**: (executed for two CLK cycles)
```
.=0  
JMP(R1)  
ADDC(R0, 1, R1)
```

**Program 6**: (executed for two CLK cycles)
```
.=0  
LDR(R31, .+8, R0)  
ADDC(R0, 1, R1)  
x : LONG(3)
```






<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIzMzUzNDIzNiwtNDUwNzk2OTEwLDEyNj
MzNjMyNTQsLTQ2NDczMzc2MywxMjQyNTQwOTA5LDcyODI4NDI1
OCwyMDY3ODkzNzI1LC0xMTIwNDM5Nzg1XX0=
-->