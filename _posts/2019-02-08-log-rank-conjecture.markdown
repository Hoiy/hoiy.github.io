---
layout: post
title:  "Introduction to the Log-rank Conjecture"
date:   2019-02-08 11:58:00 +0800
categories: [research, log-rank-conjecture]
published: true
---
Log-rank conjecture is one of the biggest and fundamental open problems in communication complexity.

Roughly speaking, Alice with input $$x$$ and Bob with input $$y$$ are trying to compute a function $$f(x, y)$$. We are interested in how many bits do they need to communicate before any of them get the result in the worst case. We denoted this as $$CC(f)$$, the communication complexity of the function $$f$$.

For simplicity, we consider only Boolean functions where Alice and Bob both holds an $$n$$ bit input:

$$f: \{0, 1\}^n \times \{0, 1\}^n \rightarrow \{0, 1\}$$

Let's take a look at a few examples to get some feeling on this complexity measure.

<br><br>
# Function with high communication complexity
**Equality**

For example, the "equality" function, denoted as

$$
\text{EQ}(x, y) = \begin{cases}
      1, & \text{if}\ x=y \\
      0, & \text{otherwise}
    \end{cases}
$$

has communication complexity $$CC(\text{EQ}) = n$$. Informally speaking, to compute $$\text{EQ}$$, it is essential for Alice or Bob to collect all the bits of others. Otherwise, we won't know for sure whether $$x$$ and $$y$$ really equals.

**Or, And**

Both $$\text{OR}$$ and $$\text{AND}$$ function has communication complexity $$CC(\text{OR}) = CC(\text{AND}) = n$$, where

$$
\text{OR}(x, y) =\begin{cases}
      1, & \text{if any input bit is 1}\  \\
      0, & \text{otherwise}
    \end{cases}
$$

$$
\text{AND}(x, y) =\begin{cases}
      1, & \text{if all input bits are 1}\  \\
      0, & \text{otherwise}
    \end{cases}
$$


With a simple adversary argument, we know that in the worst case, Alice or Bob must examine the very last bit from other before they could compute the final result with certainty.

<br><br>
# Function with low communication complexity
**Parity**

Let's take a look at another function "parity"

$$\text{PARITY}(x, y) = x_1 \oplus ... \oplus x_n \oplus y_1 \oplus ... \oplus y_n$$

which has communication complexity $$CC(\text{PARITY}) = 1$$. Alice in this case could just sends her 1 bit parity result on $$x$$ to Bob.

**Address**

Alice holds an input $$x$$ of size $$\log n$$, Bob holds an input $$y$$ of size $$n$$.

$$\text{ADDR}(x,y) = y_x$$

We have $$CC(\text{ADDR}) \leq \log n$$ by having Alice sending her "address" bits to Bob.

**Halting Problem**

Alice holds an input $$x$$, Bob holds an input $$y$$ which is the code of a Turing Machine $$M_y$$. The function

$$
\text{HALT}(x, y) = \begin{cases}
  1, & \text{if}\ M_y \text{ halt on input } x \text{ and } x = 1^n \\
  0, & \text{otherwise}
\end{cases}
$$

has communication complexity $$CC(\text{HALT}) = 1$$. This is done by having Alice to send a one-bit signal indicating whether her input is $$1^n$$ to Bob.

This showcase that when we are working on communication complexity, we don't make any assumption on the computation power of Alice and Bob. They are capable of solving the halting problem or doing even more. We only care about how many bits do they need to communicate in the worst case.

<br><br>
# The log-rank conjecture

Give a function $$f$$, we could write down its communication matrix $$M_f$$ of size $$2^n$$ by $$2^n$$, where $$M_f[x, y] = f(x, y)$$. The rank of this matrix is denoted as $$\text{rank}(M_f)$$. Log-rank conjecture states that

**Log-rank conjecture** For all Boolean function $$f$$, there exists a universal constant $$c$$ such that

$$CC(f) = O(\log^c \text{rank}(M_f))$$

The Log-rank conjecture remains an unsolved open problem. In the past few years, there are great processes toward solving this conjecture and its variance. In the next post, we would like to look at a very recent result, that [the log-approximate-rank conjecture is False](https://eccc.weizmann.ac.il/report/2018/176/).
