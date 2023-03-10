Here's an interesting thing about the Collatz conjecture. If you want to find cycles for a specific rule, $m * x + s$, that passes through a certain number of odd numbers, we can find them using a simple formula (or prove they don't exist).

For long-ish cycles (with $n >> s$, where $n$ is the number of odd numbers in the cycle) we can use the formula:

$a = s * \frac{m^{n-1} + 2^i * m^{n-2} + 2^{i+j} * m^{n-3} + ... 2^{i + j + .. y}}{2^{i + j .. y + z} - m^{n}}$

Where $a$ is one of the odd numbers, $n$ is the number of odd numbers in the cycle, and $i, j, ... y, z$ are powers of 2 such that $i+j+..+y+z = floor(log_2(m^n))+1$ and $i, j, .. y, z$ are positive integers. If $a$ is a positive odd number then we've found a cycle. 

You can also find cycles using this formula. If $s = 2^{floor(log_2(m^n))+1} - m^n$ then $a$ is always a whole number. So, given any arbitrary valid $m$ and $n$, we can always find an integer $s$ to plug in that gives a cycle.

Example, for the rule $3 * x + s$ and $n=5$, plugging in, we get $s=13$ and indeed, plugging in, there are cycles, such as one including $341$  or $211$. 

In order for $3 * n + 1$ to have a cycle in the above formula, we need $\frac{3^{n-1} + 2^i * 3^{n-2} + 2^{i+j} * 3^{n-3} + ... 2^{i + j + .. y}}{2^{i + j .. y + z} - 3^{n}}$ to be a postive whole number. That doesn't seem to be possible, but I can't exactly say why!
