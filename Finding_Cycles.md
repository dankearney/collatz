# Quick proof

Suppose there is a cycle of numbers $n_1$, $n_2$, $n_m$ of length $m$, where $n_m = n_1$. Define $n_1$ as the smallest odd number in the cycle.

Each number $n_i$ is either $n_{i-1} * \frac{1}{2}$ or $3 + \frac{1}{n_{i-1}} * n{i-1}$. If there are $e$ even numbers and $o$ odd numbers in the cycle, then, the increases of $3 + \frac{1}{n_i}$ for each odd number must have the same product as the decreases of halving. Substituting that in, $\frac{1}{2}^{e} = (3 + \frac{1}{n_{o_{1}}}) (3 + \frac{1}{n_{o_2}}) ... (3 + \frac{1}{n_{o_{max}}})$.

A cycle requires each $n_i$ to be distinct odd values such that the RHS product of $o$ terms exactly equals the LHS, which is $2^e$. Since the odd numbers in a cycle are constrained, we can find an upper limit for at least one value in the cycle of any length. Interestingly this limit does not grow with longer cycle lengths. 

# Quick Summary

The Collatz Conjecture is simple on the surface. Given any number, $n_0$, if it's even, divide it by 2, if it's odd, increase it by $3 * n_0 + 1$. The conjecture states that all starting numbers wind up back at 1. This post explains why there are no cycles besides the trivial 1 => 4 => 2 => 1. 

For a cycle to exist as you move from one number to another to another, the product of all of the increases must equal the decreases — i.e. after all the ups and downs, you need to wind up exactly where you started.

For example, for the rule where odd numbers go up by $3 * n + 5$, one cycle is 19 => 62 => 31 => 98 => 49 => 152 => 76 => 38 => 19. The increases here are approximately 3.26, 3.16, and 3.10, the product of which is exactly 32, or $2^5$, which is also the product of the decreases!

As n gets larger, $\frac{3 * n + 1}{n}$ approaches $3$. n=10,001 to 30,004 is an increase of 3.0001, for example. So as $n$ gets larger, the product of the increases is close to a power of 3, and that has to exactly equal a power of 2. 

As you try ever larger values of n, you need ever larger cycle lengths to get the increases to compound such that you move away from a power of 3 and towards a power of 2. This is why all the cycles you can find for various rules tend to be of smaller $n$ and shorter cycle length -- otherwise you'll need to find a starting number such that you have a preposterously long cycle.

# Background

The Collatz conjecture is interesting for two reasons: first, that the traversal never winds up going up to infinity, it always goes down. That part is not super exciting, because the probabilistic explanation is that the division by 2 of even numbers is stronger than the increase of $3 * n + 1$ (and its subsequent halving, since that's always even) over the long run, so a decrease is inevitable. The more interesting problem is why there are no cycles -- that is, why you never get stuck in a loop, besides the trivial $4 => 2 => 1 => 4$. 

This approach focuses on an explanation for the lack of cycles. 

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

## Finding the Largest Viable Starting Point for a Cycle Length

For a 3-odd cycle, we can set a hard upper limit on the lowest odd number in the cycle with this approach by finding the nearest power of 2 and the largest possible starting point for the optimal cycle.  

A 3-odd cycle is going to have a product of increases above 27, so the easiest power of 2 to reach is $2^5 = 32$. 

$n_{o_1}$, $n_{o_2}$ and $n_{o_3}$ cannot be arbitrary numbers, they must be unique odd numbers in a valid sequence. We are looking to maximize the product of the increases, which means computing the optimal sequence of decreases of powers of 2 to maximize the product. Assuming we can find a generic solution to that problem, we can iteratively compute the lowest value in a cycle that actually makes the product >= 32. For the 3-odd cycle approach we need $o_{n_1}$ to be 3 in order for the product to be above 32; that's our hard upper limit. Never mind if 3 actually works -- we just want that upper limit for one of the values. For any cycle length, we can use this approach of alternativng between increases of 2 and decreases of 4 to find a hard upper limit for any cycle length. As it turns out, this hard upper limit does not grow over time, instead stabilizing. While this is not a proof, it is certainly interesting.
