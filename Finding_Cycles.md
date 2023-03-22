# Quick Summary

As you traverse from one number (n0) to another (n1), n1 is either n0/2 or (3 n0 + 1). For a cycle to exist, the product of all of the increases must equal the decreases — you need to wind up exactly where you started.
For example, the trivial cycle 1 => 4 => 2 => 1 has one increase of (3 + 1) = 4, and two decreases of 2, also equaling 4.

For the alternative rule where odd numbers go up by 3n + 5, there are some cycles, like 19 => 62 => 31 => 98 => 49 => 152 => 76 => 38 => 19. The increases here are approximately 3.26, 3.16, and 3.10, the product of which is exactly 32, or 2^5.

As n gets larger, (3n + 1) approaches 3n. n=10,001 to 30,004 is an increase of 3.0001, for example. So as n gets larger, the product of the increases is near a power of 3, and that has to exactly equal a power of 2.

For small cycles with just a few odd numbers, this number is quite close to a power of 3. 3.0001^4, for example, is 81.01, a tiny bit larger than 81. Clearly, we need a big cycle with a lot of odd numbers so that the little error gets magnified. However, as the power of 3 gets larger, the next nearest power of 2 remains far away, as explained here. https://mathoverflow.net/a/116960

So, as you try ever larger values of n, you need ever larger cycle lengths to get the increases to produce a power of 2, but that power of 2 gets ever farther away. This is why all the cycles you can find for various rules tend to be of smaller n.

# Background

The Collatz Conjecture is simple on the surface. Given any number, $n_0$, if it's even, divide it by 2, if it's odd, increase it by $3 * n_0 + 1$. The conjecture states that all starting numbers wind up back at 1. This is interesting for two reasons: first, that the traversal never winds up going up to infinity, it always goes down. That part is not super exciting, because the probabilistic explanation is that the division by 2 of even numbers is stronger than the increase of $3 * n + 1$ over the long run, so a decrease is inevitable. The more interesting problem is why there are no cycles -- that is, why you never get stuck in a loop, besides the trivial $4 => 2 => 1 => 4$. 

My approach focuses on an explanation for the lack of cycles. 

Given any $n_0$, we can write $n_1$ as $n_1 = \alpha_0 * n_0$, where $\alpha_0$ either equals $\frac{1}{2}$ (for even numbers) or $\frac{3 * n_0 + 1}{n_0}$ (for odd numbers). 

The next number, $n_2$, can be written again as $n_2 = n_1 * \alpha_1$, or $n_2 = \alpha_0 * \alpha_1 * n_0$. Generalizing, $n_i = \alpha_0 * \alpha_1 ... * alpha_i * n_0$. A cycle has $n_n = n_0$, so $n_0 = \alpha_0 * \alpha_1 * ... \alpha_i * n_0$. Canceling out the $n_0s$ we can move all of the $\frac{1}{2}$ to the left side, and keep the odd alphas on the right. Then, we have:

$2^{number evens} = \frac{3 * n_{odd_1} + 1}{n_{odd_1}} * \frac{3 * n_{odd_2} + 1}{n_{odd_2}} ... * \frac{3 * n_{odd_m} + 1}{n_{odd_m}}$

This expression means that the product of the increases of $3 * n + 1$ has to exactly equal the product of the decreases by half. Another way of saying it is that the increases must have a product that is exactly a power of 2.

## Examples

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
