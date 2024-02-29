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
  
  **$$T(n) \in \Theta(\log(n))$$**

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
  
  **$$T(n) \in \Theta(n)$$**

  


3.
$$ T(n) =
    \begin{cases}
        1 & n \leq 1\\
        13 T\left(\frac{n}{13}\right) + 2n & n > 1
    \end{cases}
$$

## Using Substitution Method:
### Recursive Expansion

To observe the pattern of the recurrence, we expand the relation:

Initial step: $T(n) = 13T(n/13) + 2n$

By substituting $T(n/13)$ back into the equation, we get an expanded form:
   $T(n) = 13^2T(n/13^2) + 2n + 2n$
   
### Identifying the Pattern of Expansion
After k expansions, the recurrence relation takes the form:
$T(n) = 13^kT(n/13^k) + 2kn$

### Reaching the Base Case

The base case is reached when $n/13^k = 1$, which means $k = log$<sub>$13$</sub>$(n)$.

### Substituting $k$ into the Expansion

Substituting $k = log$<sub>$13$</sub>$(n)$ back into our expanded equation, we get:

$T(n) = n + 2nlog$<sub>$13$</sub>$(n)$

### Simplifying

This simplifies to a growth of $Θ(n log n)$, showing the solution's complexity:

**$$T(n) \in \Theta(n \log(n))$$**


## Verifying with Master Theorem

The Master Theorem helps us find the time complexity of recurrence relations of the form:
$T(n) = aT(n/b) + f(n)$
- **a** is how many times the function calls itself.
- **b** is how much smaller each recursive call's input size is.
- **f(n)** is the extra work done outside the recursive calls.

### Matching Given Equation to the Theorem

For our recurrence relation:
- $a = 13$, because the function calls itself 13 times.
- $b = 13$, because each time, the input size is divided by 13.
- $f(n) = 2n$, the extra work for combining the results.

### Analyzing $f(n)$ Against $n$<sup>$(log_b(a))$</sup>

- We calculate $log_b(a)$ = $log$<sub>$13$</sub>$(13) = 1$.
- So, we compare $2n$ (our $f(n)$ ) with $n^1$ (which is just $n$).

### Applying Master Theorem

According to the theorem, we have three cases. Our case matches when $f(n)$ is directly proportional to $n$<sup>$(log_b(a))$</sup>, which puts us in **Case 2**:

- **Case 2** of the Master Theorem says if $f(n)$ = $Θ(n$<sup>$(log_b(a))$</sup>), then the overall complexity is $Θ(n$<sup>$(log_b(a))$</sup> * $log n$).

### Concluding Complexity

Since $f(n) = 2n$ matches $n$<sup>($log$<sub>$13$</sub>($13$))</sup> = $n$, by Case 2, we find:
- $T(n) \in \Theta(n \log(n))$

### Conclusion

By applying the Master Theorem to the recurrence relation, we find that the computational complexity is $Θ(n * log n)$. This means as the size of our problem ($n$) increases, the total work or time to solve the problem grows in proportion to $n * log n$.

**$$T(n) \in \Theta(n \log(n))$$**

