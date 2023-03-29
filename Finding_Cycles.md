# Quick proof

Suppose there is a cycle of numbers $n_1$, $n_2$, $n_m$ of length $m$, where $n_m = n_1$. Define $n_1$ as the smallest odd number in the cycle.

Each number $n_i$ is either $n_{i-1} * \frac{1}{2}$ or $3 + \frac{1}{n_{i-1} * n{i-1}. If there are $e$ even numbers and $o$ odd numbers in the cycle, then, the increases of $3 + \frac{1}{n_i}$ for each odd number must have the same product as the decreases of halving. Substiting that in, $\frac{1}{2}^{e} = (3 + \frac{1}{n_{o_{1}}}) (3 + \frac{1}{n_{o_2}}) ... (3 + \frac{1}{n_{o_{max}}})$.

A cycle requires each $n_i$ to be distinct odd values such that the RHS product of $o$ terms exactly equals the LHS, which is $2^e$. 

Let's try to find a cycle. If $o=3$, the cycle has 3 odd numbers. Since each $3 + \frac{1}{n_1} \approx 3 $ except for trivially small $n_i$, the RHS will be somewhat larger than $3^3 = 27$. The nearest viable power of 2 is $2^5 = 32$. So, $n_{o_1}$, $n_{o_2}$, and $n_{o_3}$ must satisfy $(3 + \frac{1}{n_{o_1}})(3 + \frac{1}{n_{o_2}})(3 + \frac{1}{n_{o_3}}) = 32$. Trying $n_1 = 1, n_2=3, n_3=5$ gives 42.667, $n_1=3, n_2=5, n_3=7$ gives 33.524, and $n_1=5, n_2=7, n_3=9$ gives 31.287. Every other combination of $n_1$, $n_2$, and $n_3% will give a smaller number above 27 -- so there is no valid $n_1$, $n_2$, and $n_3$ that can give a 3-odd cycle. 

Extending this out to arbitrary lengths.


# Quick Summary

The Collatz Conjecture is simple on the surface. Given any number, $n_0$, if it's even, divide it by 2, if it's odd, increase it by $3 * n_0 + 1$. The conjecture states that all starting numbers wind up back at 1. This post explains why there are no cycles besides the trivial 1 => 4 => 2 => 1. 

For a cycle to exist as you move from one number to another to another, the product of all of the increases must equal the decreases — i.e. after all the ups and downs, you need to wind up exactly where you started.

For example, for the rule where odd numbers go up by $3 * n + 5$, one cycle is 19 => 62 => 31 => 98 => 49 => 152 => 76 => 38 => 19. The increases here are approximately 3.26, 3.16, and 3.10, the product of which is exactly 32, or $2^5$, which is also the product of the decreases!

As n gets larger, $\frac{3 * n + 1}{n}$ approaches $3$. n=10,001 to 30,004 is an increase of 3.0001, for example. So as $n$ gets larger, the product of the increases is close to a power of 3, and that has to exactly equal a power of 2. 

As you try ever larger values of n, you need ever larger cycle lengths to get the increases to compound such that you move away from a power of 3 and towards a power of 2. This is why all the cycles you can find for various rules tend to be of smaller $n$ and shorter cycle length -- otherwise you'll need to find a starting number such that you have a preposterously long cycle.

# Background

The Collatz conjecture is interesting for two reasons: first, that the traversal never winds up going up to infinity, it always goes down. That part is not super exciting, because the probabilistic explanation is that the division by 2 of even numbers is stronger than the increase of $3 * n + 1$ (and its subsequent halving, since that's always even) over the long run, so a decrease is inevitable. The more interesting problem is why there are no cycles -- that is, why you never get stuck in a loop, besides the trivial $4 => 2 => 1 => 4$. 

My approach focuses on an explanation for the lack of cycles. 

Given any $n_0$, we can write $n_1$ as $n_1 = \alpha_0 * n_0$, where $\alpha_0$ either equals $\frac{1}{2}$ (for even numbers) or $\frac{3 * n_0 + 1}{n_0}$ (for odd numbers). 

The next number, $n_2$, can be written again as $n_2 = n_1 * \alpha_1$, or $n_2 = \alpha_0 * \alpha_1 * n_0$. Generalizing, $n_i = \alpha_0 * \alpha_1 ... * alpha_i * n_0$. A cycle has $n_n = n_0$, so $n_0 = \alpha_0 * \alpha_1 * ... \alpha_i * n_0$. Canceling out the $n_0s$ we can move all of the $\frac{1}{2}$ to the left side, and keep the odd alphas on the right. Then, we have:

$2^{evens} = \frac{3 * n_{odd_1} + 1}{n_{odd_1}} * \frac{3 * n_{odd_2} + 1}{n_{odd_2}} ... * \frac{3 * n_{odd_m} + 1}{n_{odd_m}}$

This expression means that the product of the increases of $\frac{3 * n + 1}{n}$ has to exactly equal the product of the decreases by half. Another way of saying it is that the increases must have a product that is exactly a power of 2.

## Examples

There are plenty of examples of cycles for other rules besides $3 * n + 1$. 

Odd rule: 5 * n + 5
Cycle: 5 => 30 => 15 => 80 => 40 => 20 => 10 => 5
Product of increases: $30/5 * 80/15 = 32$
Product of decreases: $2^5 = 32$

Odd rule: 5 * n + 9
Cycle: 64 => 32 => 16 => 8 => 4 => 2 => 1 => 14 => 7 => 44 => 22 => 11 => 64
Product of increases: $14/1 * 44/7 * 64/11 = 512$
Product of decreases: $2^9 = 512$

Odd Rule: 1 * n + 9
Run: 7 => 16 => 8 => 4 => 2 => 1 => 10 => 5 => 14 => 7
Product of increases: $16/7 * 10 / 1 * 14 / 5 = 64$
Product of decreases: $2^6 = 64$

## Near-Cycles

The $3 * n + 1$ rule has some near-cycles, like 59 => 178 => 89 => 268 => 134 => 67 => 202 => 101 => 304 => 152 => 76 => 38 => 19 => 58. 

The increases here as we move from odd to even are 178/59=3.017, 268/89=3.011, 202/67=3.015, 304/101=3.001, and 58/19=3.053, the product of which is 251.66 -- reasonably close to the product of the decreases (256), but not exactly equal, hence that this is not a cycle. 

## The Futility of Trying to Find Cycles

The Collatz conjecture is known to be true for some gigantic numbers. This means any cycle must start with a very large number, which also implies that $\frac{3 * n + 1}{n}$ is extremely close to $3$.   For n=1 billion, $\frac{3 * n + 1}{n} =  3.000000001$, for example.

If the cycle has $d$ odd numbers, then the upper limit of the product of the increases is $3 + x^d$, where $x$ is the largest excess over 3.0. $x < 1$ and approaches 0.  

Best case scenario, there is a power of 2 that is exactly 1 larger than $3^d$ and we just need $3 + x^d = 3^d + 1$.

For $n=$ 1 billion, $x = .00000001$. The smallest value of $d$ that satisfies the above is 18, so the cycle must have at least 18 odd numbers in it. $3^18 = 387420489$, but the nearest power of 2 above that is $2^29 = 536870912$, which is 149450423 larger than the power of 3. Bad luck -- the power of 2 is nowhere nearby. But no worries, we can just try a much larger cycle to get our error to increase such that we get closer! How about $d = 100$? No dice. The next power of 2 above $3^{100}$ is $2^{159}$, which is 215373297933440128065381286592520237125858749487 above $3^{100}$ -- preposterously out of reach of even our compounding error. As the cycles get longer, the nearest power of 2 actually trends further away. Why? https://mathoverflow.net/a/116960 explains this nicely -- powers of 2 and 3 cannot be close to one another as powers get larger. We need a power of 2 to be close to a power of 3, but that is not possible. And, as we try larger starting numbers, $\frac{3 * n +1}{n}$ gets even closer to 3.0, necessitating even larger cycle lengths, making the problem worse!

What does this mean? Cycles must be relatively short, and start with relatively low numbers, otherwise the product of the increases must be 
