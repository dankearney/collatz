Here's an interesting thing about the Collatz conjecture. If you want to find cycles for a specific rule, $m * n + s$, that passes through a certain number of odd numbers, it's easy to do. 

For long-ish cycles (with $n >> s$) we can use the formula:

$a = s * \frac{m^n + 2^i * m^{n-1} + 2^{i+j} * m^{n-2} + ... 2^(i + j + .. y)}{2^{i + j .. y + z}}$
