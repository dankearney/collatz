Finding Cycles in the Collatz Conjecture Universe

# Overview

I've been exploring the Collatz conjecture lately. It's always fascinated me -- it's so simple on the surface! 

I took an interest in exploring the $3 * n + s$ case, because $3 * n + 1$ having more than 1 cycle is unproven, but there are cycles for other values of $s$. For $3 * n + 7$, only a slightly different rule, there is $5 ⇧ 22 ⇩ 11 ⇧ 40 ⇩ 20 ⇩ 10 ⇩ 5$ among many other examples. So, what is so special about $ 3 * n + 1$?

In this post I deep-dive into this case and I found a neat and tidy way to find cycles for a given $3 * n + s$ rule of a specific length. This also can give an explanation for why there are no such cycles for $3 * n + 1$ above the trivial cycle.

# Approach

From any given starting number, $N_{0}$, the next number, $N_{1}$, can be represented as $N_{1} = \alpha_{0} * N_{0}$. $\alpha_{0}$ will either be $\frac{1}{2}$ (for even numbers) or $\frac{3 * N_{0} + s}{N_{0}}$ (for odd numbers). If $N_{1}$ is even again, then we can just skip down to the next number and replace $alpha_{0} = \frac{1}{2}$ with $\alpha_{0} = \frac{1}{4}$, and so on, until we reach an odd number. $N_{2}$, then, is $N_{1} * \alpha_{1}$, or, $N_2 = N_{0} * \alpha_{0} * \alpha_{1}$. Extending this out, $N_{n} = \alpha_{0} \alpha_{1} ... \alpha_{n} * N_{0}$. 

$\alpha_{i}$ is either a fractional power of 2 (for even numbers) $\frac{1}{2}^{i}$, where ${i}$ is some positive integer, or $\frac{3 * a+ s}{a}$, where $a$ is some positive odd integer. This means that the n'th number can be determined by:

$N_{n} = \frac{1}{2}^{i} \frac{1}{2}^{j} ... \frac{1}{2}^{t_{max}} \frac{3 * a + s}{a} \frac{3 * b + s}{b} ... \frac{3 * o_{max} + s}{o_{max}}$.

The value of $\frac{3 * o_{i} + s}{o_{i}}$ is not a constant but is different for every odd number, however, it approaches $3$ as $o$ gets larger than $s$, and for $o=1$ it is simply $3+s$.  

# Finding cycles

A cycle is found when the n'th number has already been visited. We can write this as $N_{n} = N_{0}$ and plugging into the above formula:

$N_{0} = \frac{1}{2}^{i} * \frac{1}{2}^{j} ... \frac{1}{2}^{t_{max}}  * \frac{3 * a + s}{a} \frac{3 * b + s}{b} ... \frac{3 * o_{max} +  s}{o_{max}} N_{0}$.

which reduces to

$2^{i} 2^{j} ... 2^{t_{max}} = \frac{3 * a + s}{a} \frac{3 * b + s}{b} ... \frac{3 * o_{max} + s}{o_{max}}$.

Intuitively, this makes sense because it's saying that the product of all of the increases (from \frac{$3 * n + s}{n}$) have to exactly match the product of all of the decreases (from halving) to get exactly back to where you started!

Each increase is near 3.0 (once you get to sufficiently large $n$) so the increase in value's lower limit is a power of 3. That means $2^{i+j...t_{max}} must be a little bit larger than a power of 3, once $n$ gets substantially larger than $s$. For a cycle with 5 odd numbers, $3^5 = 243$ and the next largest power of 2 is $2^8% or 256. In math terms, we can reasonably assume $t_{max} = floor(log2(3^{o_{max}}$. 

Let's see if this works. Let's try the classic $3 * n + 1$. We know there is a cycle $1 ⇧ 4 ⇩ 2 ⇩ 1$. From 4 to 1 is a decrease of $2^2$ or 4, and the increase is $\frac{3 * 1 + 1}{1}$ or 4, and $4=4$, so this works.

For a longer cycle, say, for the rule $3 * n + 7$, $5 ⇧ 22 ⇩ 11 ⇧ 40 ⇩⇩⇩ 5$, we can see that the product of the increases does equal the product of the decreases:

$\frac{3 * 5+7}{5} * \frac{3 * 11+7}{11} = 2^{1} * 2^{3} = 16$

# A mathematical way to find cycles

Using this formula we can re organize a bit to make an expression we can use to actually find cycles! This means, given a rule, we can plug in a length of a cycle (in terms of how many odd numbers) and it will tell us all of the starting points of such a cycle, or if such a cycle doesn't exist.

## 2 Odd Number Cycle

Equation 1: $2^{i} 2^{j} = \frac{3 * a + s}{a} \frac{3 * b + s}{b} $

Also, we know that every odd number (a, b, etc) is the previous odd number, increased by 3n+s, and divided by 2, 4, 8 or some other power of two. Writing this out for a 2-odd-cycle:

Equation 2: $b = \frac{3 * a + s}{2^i}$

Equation 3: $a = \frac{3 * b + s}{2^j}$

Substiting $a$ into equation 1:

$2^{i} 2^{j} = \frac{3 * a + s}{a} \frac{3 * \frac{3 * a + s}{a * 2^i} + s}{\frac{3 * a + s}{a * 2^i}} $

Solving for $a$

$a = s * \frac{(3 + 2^i)}{2^{j+i} - 3^2}$ 

For a 2-cycle, we know that the increase is larger than $3^2 = 9$ so the decreases are likely to be the next power of 2, which is 16. 16 can be reached in 3 ways with a cycle of 2 odd numbers, either $2^1 * 2^3$ or $2^2 * 2^2$ or $2^3 * 2^1$. Plugging these possible values of $i$ and $j$, we get $a = 5, a=11, a=7$. These are indeed all 2-cycles:

$5 \uparrow 22 \downarrow 11 \uparrow 40 \downarrow 20 \downarrow 10 \downarrow 5$, which includes both 5 and 11 

$7 \uparrow 28 \downarrow 14 \downarrow 7$ is a 1-cycle, but it's also a 2-cycle if you loop through it twice!

## Generalizing

If we run the above math again for a 3-odd cycle we get a similar expression, which we can generalize to an n-cycle.

Equation 1: $2^{i} 2^{j} 2^{k} = \frac{3 * a + s}{a} \frac{3 * b + s}{b} \frac{3 * c + s}{c}$

Equation 2: $b = \frac{3 * a + s}{2^i}$

Equation 3: $c = \frac{3 * b + s}{2^j}$

Equation 4: $a = \frac{3 * c + s}{2^k}$

Substituting and solving for $a$

$2^{i} 2^{j} 2^{k} = \frac{3 * a + s}{a} \frac{3 * \frac{3 * a + s}{2^i} + s}{\frac{3 * a + s}{2^i}} \frac{3 * \frac{3 * \frac{3 * a + s}{2^i} + s}{2^j} + s}{\frac{3 * \frac{3 * a + s}{2^i} + s}{2^j}}$ 

Solving for $a$

$a = s * \frac{3^2 + 3 * 2^i + 2^{i+j}j}{2^{i+j+k} - 3^3}$

(Quickly testing this out for $3 * n + 5$, we get $a=19, a=49, a=31, a=37, a=23, a=29$, which is correct. 

Generalizing to a n-cycle:

$a = s * \frac{3^{n-1} + 3^{n-2} * 2^i + 3^{n-3} * 2^{i+j} ... + 3^{0} * 2^{i + j + ... + y}{2^{i+j .. + y + z} - 3^n}$ where $i + j + ... y + z = floor(log2(3^m))+1$ when $n >> s$.

TODO: Python script with examples

# The $3 * n + 1$ case

For $3 * n + 1$, the expression is simplified a bit because $s=1$. Rearranging a bit... 

${2^{i+j .. + y + z} - 3^n} = \frac{3^{n-1}}{a} + \frac{3^{n-2} * 2^i}{a} + \frac{3^{n-3} * 2^{i+j}}{a} ... + \frac{3^{0} * 2^{i + j + ... y}}{a}$

## Observations

Notice that in the numerator, $i, j, k$ are present but the final power of 2 ($z$) is not in the numerator, just the denominator. A perfectly valid cycle would be $i=1, j=1, k=1$ etc and then $z$ is some large number. For this particular cycle, we can rewrite the above formula as

${2^{i+j .. + y + z} - 3^n} = \frac{3^{n-1} + 3^{n-2} * 2 + 3^{n-3} * 2^2 ... + 3^{0} * 2^{n-1}}{a}= \frac{\product{a}{b}}{a} $

## Back to the general case

${2^{i+j .. + y + z} - 3^n} = \frac{3^{n-1}}{a} + \frac{3^{n-2} * 2^i}{a} + \frac{3^{n-3} * 2^{i+j}}{a} ... + \frac{3^{0} * 2^{i+j+y}}{a}$

Left side of the equation is a whole number, so the right hand terms sum to a whole number. 

Note that each term in the RHS is a fraction, where the numerator is of the form $3^n * 2^m$. $a=1$ gives the trivial cycle so another cycle must be larger than $a=1$.

Since the left hand side is a whole number, so is the right hand side. To make that happen, $a$ needs to either:

1: Evenly divide all the terms so each term is a whole number

2: Divide some or all of the numbers evenly, and for the terms that are not divided evenly, their remainders must sum to a whole number. 

(1) is impossible because $a$ would need to evenly divide both a power of 3 and a power of 2.

(2) $a$ will never divide $2^{i+j+..+y}$ evenly because that would imply $a$ is even. So, there will always be a remainder, of the form $\frac{r}{2^{i+j+...y}}$. At least one of the other terms must also have a remainder in order to offset this remainder to sum to a whole number. Summing these other remainders to a single fraction, we will have $\frac{R}{3^j * 2^k}$. $R$ is even. $r$ is odd.  These two irreducible fractions cannot be added to make a whole number because $r$ and $R$ are not both even or both odd. 
