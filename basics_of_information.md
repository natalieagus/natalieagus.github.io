---
layout: default
permalink: /50002/1
---

<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>


50.002 Computational Structures
Information Systems Technology and Design
**Natalie Agus (Fall 2020)**

# Basics of Information Theory

You can download the .pdf for this notes [here](https://www.dropbox.com/s/bhzkwfxy0aw4k0w/BasicsOfInformation.pdf?raw=1).

## Overview

In this course, we are going to learn about how the computer works from the **bottom up**. We will begin with discovering how can we represent and encode *information*, and then followed by how we can store this information in a tangible form using voltages (next lecture).

## Information and uncertainty


The amount of information  (required/needed/given/revealed/acquired)* is **inversely proportional to** the probability $p$ of that event
happening,

$$\begin{aligned}
\text{Information } \propto \text{ Uncertainty} \propto \text{ }\frac{1}{p}.\end{aligned}$$

Equivalently, it is **proportional to** the uncertainty of that event
happening. 


<mark>In laymen terms: *If an event is bound to happen, then the fact that the event happens does not give any kind of information*</mark>

For discrete events $(x_1, x_2, ... , x_N)$ with probability of occurence of $(p_1, p_2, ..., p_N)$, the basic measure of information for all of these events is the ***bit***.  

How many bits is needed to reveal that a random variable is $x_i$?

$$\begin{aligned}
I(X) =  \log_2 \frac{1}{p_i} \text{ bits},\end{aligned}$$

where:  $I(X)$ is the amount of information received in bits learning that the choice was $x_i$.   With $N$ equally probable choices, if it is narrowed down to $M$ choices ($N>M$), then we are given,

$$\begin{aligned}
I_{N\rightarrow M}(X) = \log_2 \left( \frac{N}{M} \right) \text{ bits},\end{aligned}$$

of information.  
 

> Example:   Let $N = 4$, and all 4 events are equally probable. The number of bits needed to encode all 4 events are: $$\begin{aligned}
> I(X) &= \log_2 \frac{1}{1/4} = 2 \text{ bits}. %H(X) &=  \sum_{i=1}^4
> \frac{1}{4} \log_2 \frac{1}{1/4} = 2 \text{bits}\\\end{aligned}$$ We need to receive 2 bit of informations to learn that one event $x_i$ out of the 4 events happens. In this case, it can be $(0,0), (0,1), (1,0)$, or $(1,1)$.

## Fixed Length Encoding (FLE)


The FLE is used in practice when all choices $x_i$ are **equally probable**.  
 
**Decimal** : 4-bit to represent 1 to 10
**Characters**: 7-bit ASCII for 86 english characters
**16-bit unicode**: for other language alphabets that are fixed, e.g:
Russian, Korean

How do we encode numbers in binary? Suppose we have binary number:

    0 0 1 1 0 1 

The above means
$0 \times 2^5 + 0 \times 2^4 + 1 \times 2^3 + 1 \times 2^2 + 0 \times 2^1 + 1 \times 2^0 = 13$ in decimal. 


What if encoding in binary is too long on paper? We can encode in **octal** (groups of 3 binaries) or **hex** (groups 4 binaries). See the table below to find out the conversion between binary, octal, hex, and decimal.

<img src="https://www.dropbox.com/s/ariqv8mky94edtm/table.png?raw=1"  width="200"  height="400" />

> **Example 1:**
> 
>  1. Binary : 101 101 101 111
>  2.  Octal : $5557_8$
>  3.  Decimal : 2927
>  4.  Hex: $0xB6F$
> 
> **Example 2:**
> 
>  1. Binary : 111 110 101
>  2. Octal : $765_8$
>  3.  Decimal : 501
> 4.  Hex (pad the MSB of the binary so that it's the closest divisible by 4, in this case, we expand from 9 bits to 12 bits)
>     $\rightarrow$ `0001 1111 0101,` hence `0x1F5`


## 2's Complement


The purpose: so we can subtract using addition. How to make 2's complement:

 - **Step 1**: inverse all $0$s into $1$s and vice versa on the original binary number
- **Step 2:** add 1 **to the number in step 1**

> **Example:** 
> `0 0 1 1 = 3` $\rightarrow$ we want to turn this into -3, so we do the steps below: 
> **Step 1**: 1 1 0 0 (inversed)\
> **Step 2**: 1 1 0 0 + 0 0 0 1 = 1 1 0 1 (add 1)
> The value of the result of step 2 above is : $-2^3 + 2^2 + 2^0 = -3$.

**Signed bit**: we define the signed bit as the <mark> most significant bit </mark>. If the MSB is 1 then the number is a negative number and vice versa. 

How to encode decimal in binary? We extend our prior knowledge. Suppose we have **signed** binary number:

    1 0 0 1 . 0 0 1 1

The above means
$-1 \times 2^3 + 1 \times 2^0 + 1 \times 2^{-3} + 1 \times 2^{-4}$.

## Binary Number Range

Given $X$ bits,

1.  We can encode $2^X$ *choices, or random variables*

2.  If it is **unsigned**, we can represent the number ranged from 0 to $2^X-1$

3.  If it is **signed**, we can represent the number ranged from
    $-2^{X-1}$ to $2^{X-1}-1$

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ1NDY0NzY4NV19
-->
