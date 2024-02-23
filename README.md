[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/8KYthzwp)
# Recurrent Recurrences

Give big $\Theta$ bounds for the following recurrence relations.

1.
$$ T(n) =
    \begin{cases}
        1 & n \leq 1\\
        T\left(\frac{n}{13}\right) + 5 & n > 1
    \end{cases}
$$



### Expansion

1. **First Expansion:**
   - For $n > 1$, we start with: $T(n) = T(n/13) + 5$.

2. **Second Expansion:**
   - Apply the relation again: $T(n) = T((n/13)/13) + 5 + 5$ = $T(n/13$<sup>$2$</sup>) + $10$.

3. **i-th Expansion:**
   - Continuing this process, after i expansions: $T(n)$ = $T(n/13$<sup>$i$</sup>) + $5i$.

### Determining Depth of Recursion

- The recursion stops when the argument inside $T()$ becomes 1 or less, which is when $n/13$<sup>i</sup> ≤ 1. Solving for i, we find i = $log$<sub>$13$</sub>$(n)$.

### Final Expression

- Substituting i = $log$<sub>13</sub>(n) back into our expanded relation and knowing that $T(1) = 1$, we get the final expression:

- $T(n) = 1 + 5log$<sub>$13$</sub>$(n)$


2.
$$ T(n) =
    \begin{cases}
        1 & n \leq 1\\
        13 T\left(\frac{n}{13}\right) + 5 & n > 1
    \end{cases}
$$

### Step-by-Step Expansion

The recurrence describes a scenario where each problem of size $n$ is divided into 13 subproblems of size $n/13$, with an additional constant work of 5.

1. **First Expansion:**
   - $T(n) = 13T(n/13) + 5$.

2. **Second Expansion:**
   - Apply the recurrence to $T(n/13)$: $T(n) = 13(13T(n/13^2) + 5) + 5 = 13^2T(n/13^2) + 13 * 5 + 5$.

3. **i-th Expansion:**
   - After $i$ expansions: $T(n) = 13^iT(n/13^i) + 5(13^{i-1} + 13^{i-2} + ... + 1)$.
   - The sum is a geometric series: $S = (13^i - 1) / (13 - 1)$ = $(13^i - 1) / 12$.

4. **Termination of Recursion:**
   - Recursion stops when $n/13^i ≤ 1$, implying $n ≤ 13^i$. Solving for $i$ gives $i = log_13(n)$.

5. **Final Expansion:**
   - Substituting $i = log_13(n)$ back: $T(n) = nT(1) + 5(n - 1)/12$, with $T(1) = 1$, simplifying to $T(n) = n + 5(n - 1)/12$.

### Simplification:

The final expression simplifies to a linear relationship with $n$:  $T(n) = n + (5(n - 1))/12$
Since both terms are linear with respect to $n$, we conclude:
$T(n) = Θ(n)$


3.
$$ T(n) =
    \begin{cases}
        1 & n \leq 1\\
        13 T\left(\frac{n}{13}\right) + 2n & n > 1
    \end{cases}
$$


### Step-by-Step Solution

1. **First Expansion:**
   - For $n > 1$, we begin with: $T(n) = 13T(n/13) + 5$.

2. **Second Expansion:**
   - Applying the relation again: $T(n) = 13[13T((n/13)/13) + 5] + 5 = 13^2T(n/13^2) + 13*5 + 5$.

3. **i-th Expansion:**
   - After $i$ expansions, we obtain: $T(n) = 13^iT(n/13^i)$ + $5Σ(13^k)$ from $k=0$ to $i-1$.

### Determining When Recursion Stops

- The recursion stops when $n/13^i ≤ 1$, leading to $i = log_13(n)$.

### Final Expression Using Geometric Series

- The sum $5Σ(13^k)$ from $k=0$ to $i-1$ is a geometric series, which simplifies to: $5(13^i - 1)/(13 - 1)$.

- Substituting $i = log_13(n)$, we get: $T(n) = n + (5(n - 1))/12$.

### Simplifying for Big Theta

- Ignoring lower order terms and constants for large $n$, we arrive at: $T(n) = (17n/12) - (5/12)$.

- Thus, for large $n$, $T(n) = Θ(n)$, indicating a linear relationship between $n$ and the total work.
