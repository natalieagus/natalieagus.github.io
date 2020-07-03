---
layout: default
title: "pset1"
permalink: /50002/PS1/
---

{::options parse_block_html="true" /}
{% include toc.html %}
{::options parse_block_html="false" /}


# Basics of Information Theory
This page contains all practice questions that constitutes the topics learned in Week 1: **Basics of Information Theory** and **The Digital Abstraction**. They are grouped into three categories: basic, intermediate, and challenging. You are recommended to do all basic problem set before advancing further. 

## Warm Up

Suppose that you are to guess the value of a 16-bit number: 0x$Z_1Z_2Z_3Z_4$ You are told that the value of $Z_1$ is B. Thus you have been given [N] bits of information. What is the value of [N]?

{::options parse_block_html="true" /}
<details>
<summary markdown="span">Show Answer</summary>
  
Obviously $Z_x$ represents **4 bits** since these are in hexadecimal number system (indicated with the prefix  `0x`.) 

We are literally *told* that the first hex digit is $B = 1011$. Hence we are given **4 bits of information**.  There are still other 12 bits which values we do not know.
</details>
<br/>
{::options parse_block_html="false" /}


## Keyboard Presses -- Basic
**(a).** Bob used an enhanced keyboard that was made up of 101 keys. He told Alice that he pressed one of the letter keys. How much information did Bob give to Alice? Hint: There are 26 letters in an alphabet.

{::options parse_block_html="true" /} 
<details> 
<summary markdown="span">Show Answer</summary>

Initially, there's 101 choices. The information that Bob gave Alice
narrows down the choices into 26. The information given is therefore
$\log_2(101) - \log_2(26) = 1.958$. 
</details> 
<br/> 
{::options parse_block_html="false" /}


**(b).** Bob used an enhanced keyboard that was made up of 101 keys. He told Alice that he pressed two of the letter keys consecutively. Bob did not mention whether the two keys are the same or not. How much information did Bob give to Alice? Hint: There are 26 letters in an alphabet.

{::options parse_block_html="true" /} 
<details> 
<summary markdown="span">Show Answer</summary>

Initially, there are $101*101$ choices. 

Pressing two letter keys consecutively (might be repeated) narrows down the choices onto $26_*26$. 

Hence the information given is $\log_2(101^2) - \log_2(26^2) = 3.916$.
</details> 
<br/> 
{::options parse_block_html="false" /}

  
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU4NDUwMTU3NiwtNzUxNTg3MDc2LC0yMD
c1MDEyMTMyLDYwNTU4NDAsMTIyMDA1MjEzNyw5Nzc1NDQ5NTZd
fQ==
-->