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
   - Applying the relation again: $T(n) = T((n/13)/13) + 5 + 5$ = $T(n/13$<sup>$2$</sup>) + $10$.

3. **i-th Expansion:**
   - Continuing this process, after i expansions: $T(n)$ = $T(n/13$<sup>$i$</sup>) + $5i$.

### Determining Depth of Recursion

- The recursion stops when the argument inside $T()$ becomes 1 or less, which is when $n/13$<sup>i</sup> ≤ 1. Solving for i, we find i = $log$<sub>$13$</sub>$(n)$.

### Final Expression

- Substituting i = $log$<sub>13</sub>(n) back into our expanded relation and knowing that $T(1) = 1$, we get the final expression:

- $T(n) = 1 + 5log$<sub>$13$</sub>$(n)$

- Considering the final expression grows logarithmically and the base of the logarithm doesn't really matter for big picture complexity (since we ignore constant numbers), the overall complexity is:
  
  $T(n) = Θ(log(n))$

  This notation indicates that the growth rate of the function is logarithmic with respect to the size of the input n


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
   - Applying the recurrence to $T(n/13)$: $T(n) = 13(13T(n/13^2) + 5) + 5$ = $13^2T(n/13^2) + 13 * 5 + 5$.

3. **i-th Expansion:**
   - After $i$ expansions: $T(n) = 13^iT(n/13^i) + 5(13^{i-1} + 13^{i-2} + ... + 1)$.
   - The sum is a geometric series: $S = (13^i - 1) / (13 - 1)$ = $(13^i - 1) / 12$.

4. **End of Recursion:**
   - Recursion stops when $n/13^i ≤ 1$, implying $n ≤ 13^i$. Solving for $i$ gives $i = log$<sub>$13$</sub>$(n)$.

5. **Final Expansion:**
   - Substituting $i = log$<sub>$13$</sub>$(n)$ back: $T(n) = nT(1) + 5(n - 1)/12$, with $T(1) = 1$, simplifying to $T(n) = n + 5(n - 1)/12$.

### Simplification:

- The final expression simplifies to a linear relationship with $n$:  

- $T(n) = n + (5(n - 1))/12$

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
   - For $n > 1$, we begin with: $T(n) = 13T(n/13) + 2n$.

2. **Second Expansion:**
   - Applying the relation again: $T(n)$ = $13[13T((n/13)/13) + 2(n/13)] + 2n$ = $13^2T(n/13^2)$ + $2 * 13 * (n/13) + 2n$.

3. **i-th Expansion:**
   - After $i$ expansions, we obtain: $T(n) = 13^iT(n/13^i) + 2n(1 + 13 + 13^2 + ... + 13^{i-1})$.

### Determining When Recursion Stops

- The recursion stops when $n/13^i ≤ 1$, which happens at $i = log$<sub>$13$</sub>$(n)$.

### Evaluating the Geometric Series

- The series $1 + 13 + 13^2 + ... + 13^{i-1}$ can be summed up as: $S = (13^i - 1) / (13 - 1)$.

- Given $i = log$<sub>$13$</sub>$(n)$, this simplifies to: $S = (n - 1) / 12$.

### Final Expression

- Substituting $i = log$<sub>$13$</sub>$(n)$ and the series sum into our expansion, we get: $T(n) = n + (2n(n - 1)) / 12$.

### Simplifying for Big Theta

- After simplification, the dominant term for large $n$ is identified: $T(n) = 1/6n^2 + 5/6n$.

  Thus, the Big Theta notation is $Θ(n^2)$, indicating a quadratic relationship between $n$ and the total work.

  $T(n) = Θ(n^2)$
