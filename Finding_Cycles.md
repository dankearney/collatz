Collatz Conjecture

# Overview

I've been exploring the Collatz conjecture where a rule follows the form $n_{1}= m * n_{0}+s$ if $n_0$ is odd, and $n/2$ if $n$ is even. $m$ and $s$ are integers, representing "magnitude" and "shift". You can extend this to other rules (like other divisors than 2) but for this blog I focus on specifically $3 * n + s$.

The classic Collatz conjecture uses $m=3$ and $s=1$, and there are no known cycles beyond the trivial cycle $1 => 4 => 2 => 1$. This is interesting because other cycles exist for other $m$ and $s$, like for $3 * n + 5$ there are cycles $14 => 7 => 26 => 13 => 44 => 22 => 11 => 38 => 14$.

In this post I show a simple expression for finding cycles that traverse $o$ odd numbers, given a rule $3 * n + s$. This also can prove that no such cycle exists for a given $o$ and gives an explanation for why there are no such cycles above $o = 1$ for $3 * n + 1$.

# Approach

