Collatz Conjecture

# Overview

A rule follows the form $n_{1}= m * n_{0}+s$ if $n_0$ is odd, and $n/2$ if $n$ is even. $m$ and $s$ are integers, representing "magnitude" and "shift". You can extend this to other rules but I focus on the more classic $m * n + s$. 

The classic Collatz conjecture uses $m=3$ and $s=1$, and there are no known cycles beyond the trivial cycle $1 => 4 => 2 => 1$. This is interesting because other cycles exist for other $m$ and $s$, like for $3 * n + 5$ there are cycles $14 => 7 => 26 => 13 => 44 => 22 => 11 => 38 => 14$.

In this post I show a simple expression, given a rule $m * n + s*, traversing $o$ odd numbers, to find any cycles or prove that there are none. 

# Approach

