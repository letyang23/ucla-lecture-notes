# Lecture 3 - Discrete Random Variables

## Review from Last Class

- Countable sample spaces (e.g. flipping a coin until first head, $\Omega = \{1, 2, \dots\} = \mathbb{N}$)
- Conditional Probability: $P(A | B) = \frac{P(A \cap B)}{P(B)}$
- Law of total probability: $P(B) = P(B | A_1)P(A_1) + \dots + P(B | A_n)P(A_n)$ for a (disjoint) partition $\Omega = A_1 \cup \dots \cup A_n$
- Bayes theorem: $P(A | B) = \frac{P(B | A)P(A)}{P(B)}$
- Independence: $P(A \cap B) = P(A)P(B)$ (or more intuitively $P(A | B) = P(A)$)
- For $n > 2$ events independence requires satisfying $2^n$ equations

**Q: Is disjoint the same as independent?** No! Disjoint events cannot both occur, while independent events don't affect each other's probabilities.

## Discrete Random Variables

A discrete random variable is a function $X : \Omega \rightarrow \mathbb{R}$ that takes a finite or countable number of values $x_1, x_2, \dots$

E.g. The number in the upper face of the rolled die, the sum of two dice

**Notation:**
- $\{\omega : X(\omega) = x\} = \{X = x\}$
- $P(\{X = x\}) = P(X = x)$

## Probability Mass Function (pmf)

The pmf of a discrete random variable taking values $x_1, x_2, \dots$ is the function:

$$
p : \mathbb{R} \rightarrow [0, 1]
$$

$$
p(x) = P(X = x) \quad \text{(Sometimes also denoted } p_X(x) \text{ or } f_X(x)\text{)}
$$

If $X$ takes on the values $x_1, x_2, \dots$ then:
- $p(x_i) > 0$, and $p(x_1) + p(x_2) + \dots = 1$
- $p(x) = 0$ for all other $x$

**E.g. Fair coin flip:**
$$
X = \begin{cases} 1 & \text{Heads} \\ 0 & \text{Tails} \end{cases}
$$

$$
p(1) = \frac{1}{2}, \quad p(0) = \frac{1}{2}, \quad p(0.5) = p(\pi) = 0
$$

## Cumulative Distribution Function (cdf)

The cdf of a discrete random variable taking values $x_1, x_2, \dots$ is the function:

$$
F : \mathbb{R} \rightarrow [0, 1] \quad \text{(sometimes denoted } F_X\text{)}
$$

$$
F(x) = P(X \leq x) \quad \forall x \in \mathbb{R}
$$

If $X$ takes on the values $x_1, x_2, \dots$ then:

$$
F(x) = \sum_{x_i \leq x} p(x_i)
$$

**E.g. Fair coin flip:**
$$
X = \begin{cases} 1 & \text{Heads} \\ 0 & \text{Tails} \end{cases}
$$

$$
F(x) = \begin{cases} 0 & x < 0 \\ \frac{1}{2} & 0 \leq x < 1 \\ 1 & x \geq 1 \end{cases}
$$

Both the pmf and the cdf completely characterize all the **probabilistic** information about a random variable (two random variables can have the same pmf and cdf and be different).

## Properties of the Cumulative Distribution Function

- $F(x)$ is increasing: $x_1 \leq x_2 \Rightarrow F(x_1) \leq F(x_2)$
- $0 \leq F(x) \leq 1$, $\lim_{x \to -\infty} F(x) = 0$, $\lim_{x \to +\infty} F(x) = 1$
- $F$ is right continuous: $\lim_{\epsilon \downarrow 0} F(x + \epsilon) = F(x)$

<img src="Lecture 3.assets/Screenshot 2025-11-28 at 12.21.53 AM.png" alt="Screenshot 2025-11-28 at 12.21.53 AM" style="zoom:50%;" />

## Bernoulli Distribution

A random variable has a **Bernoulli distribution**

$$
f_X(1) = p, \quad (0 \leq p \leq 1)
$$

$$
f_X(0) = 1 - p
$$

$$
X \sim Bern(p) \quad \text{or} \quad X \sim Bernoulli(p)
$$

- Models experiments with only two possible outcomes
- E.g. coin toss (H vs. T), die comes up six (yes vs. no)
- A random variable with a Bernoulli distribution is called a **Bernoulli trial**

## Binomial Distribution

$n$ independent Bernoulli trials (e.g. flipping a coin $n$ times): $X_1, \dots, X_n \sim Bernoulli(p)$

$X = X_1 + \dots + X_n$ counts the number of successes in $n$ trials

$$
X \sim Bin(n, p) \quad \text{or} \quad X \sim Binomial(n, p)
$$

$$
f_X(k) = P(X = k) = \binom{n}{k} p^k (1-p)^{n-k} \quad k = 0, 1, \dots, n
$$

- Models the number of successes in $n$ trials
- For $n = 1$ the Binomial distribution is the Bernoulli distribution

### Example: Side Effects

Suppose it is known that 5% of adults who take a certain medication experience negative side effects. What is the probability that more than $k$ patients in a random sample of 100 will experience negative side effects?

$$
P(X > 1 \text{ patients experience side effects}) = ?
$$
$$
P(X > 5 \text{ patients experience side effects}) = ?
$$
$$
P(X > 15 \text{ patients experience side effects}) = ?
$$

### Binomial Distribution in R

pmf, cdf, and Random generation of a binomial random variable

```r
# pmf
dbinom(3, size=10, prob=0.3)
## [1] 0.2668279

# cdf
pbinom(3, size=10, prob=0.3)
## [1] 0.6496107

# Random generation
rbinom(n=1, size=10, prob=0.3)
## [1] 2

rbinom(n=3, size=10, prob=0.3)
## [1] 0 1 3
```

### Side Effects Example (continued)

$$
P(X > 1) = 1 - P(X \leq 1) = 1 - F_X(1)
$$

```r
1 - pbinom(1, size = 100, prob = 0.05)
## [1] 0.9629188

pbinom(1, size = 100, prob = 0.05, lower.tail = FALSE)
## [1] 0.9629188

pbinom(5, size = 100, prob = 0.05, lower.tail = FALSE)
## [1] 0.3840009

pbinom(15, size = 100, prob = 0.05, lower.tail = FALSE)
## [1] 3.705408e-05
```

### Binomial distribution pmf

```r
par(mar=c(6,8,5,1))

plot(0:5, dbinom(0:5, size=5, prob=0.4), col='red4', type='p', pch=16, cex=1.3, xlab='x', ylab='p(x)', cex.lab=2, cex.axis=2)
```

<img src="Lecture 3.assets/Screenshot 2025-11-28 at 12.24.33 AM.png" alt="Screenshot 2025-11-28 at 12.24.33 AM" style="zoom:50%;" />

### Binomial distribution cdf

```R
par(mar=c(6,8,5,1))

plot(stepfun(0:5, c(0, pbinom(0:5, size=5, prob=0.4))), pch = 1, lwd=2, col='steelblue', xlab='x', ylab='F(x)', cex.lab=2, cex.axis=2, main='', verticals = F)
```

<img src="Lecture 3.assets/Screenshot 2025-11-28 at 12.25.34 AM.png" alt="Screenshot 2025-11-28 at 12.25.34 AM" style="zoom:50%;" />

### Simulating a binomial 3 different ways

**Generating $n$ Bernoulli trials**

```R
Bernoulli_trials_1 = sample(0:1, 10, replace = TRUE, prob=c(0.3, 0.7))
Bernoulli_trials_1

## [1] 1 1 0 1 1 0 1 0 1 0

sum(Bernoulli_trials_1)

## [1] 6
```
**Generating $n$ Bernoulli trials using rbinom()**

```R
Bernoulli_trials_2 = rbinom(10, size = 1, prob=0.3)
Bernoulli_trials_2

## [1] 0 1 0 0 0 0 0 0 0 0

sum(Bernoulli_trials_2)

## [1] 1
```

**Directly sampling from the binomial** 

```R
rbinom(1, size=10, prob=0.3) 

## [1] 5
```

## Geometric Distribution

A discrete random variable $X$ has a **geometric distribution** with parameter $p$, where $0 < p \leq 1$, if its probability mass function is given by:

$$
p_X(k) = P(X = k) = (1-p)^{k-1} p \quad k = 1, 2, \dots
$$

$$
X \sim Geo(p) \quad \text{or} \quad X \sim Geometric(p)
$$

Models the (discrete) waiting time until an event happens. E.g. number of trials till first heads.

### Example: Concert Ticket

You and a friend want to go to a concert, but there's only one ticket left. The salesperson decides to toss a coin until heads appears. In each toss heads appears with probability $p$, where $0 < p < 1$, independent of each of the previous tosses. If the number of tosses needed is odd, your friend is allowed to buy the ticket; otherwise you can buy it. Would you agree to this arrangement?

### Geometric Memoryless Property

$$
P(X > n + k | X > k) = P(X > n)
$$

The probability it'll take $n$ additional trials if the first $k$ are failures is the same as the probability it'll take $n$ trials at the beginning of the experiment.

### Geometric Distribution in R

pmf, cdf, and Random generation of a binomial random variable

**Warning:** The definition of the geometric in R is the number of **failures before the first success**, i.e. $X - 1$.

```r
dgeom(x=5, prob = 0.1)
## [1] 0.059049

pgeom(10, prob= 0.1)
## [1] 0.6861894

rgeom(n=1, prob= 0.1)
## [1] 0

rgeom(n=3, prob= 0.1)
## [1] 4 3 4
```

#### Geometric distribution pmf

```R
par(mar=c(6,8,5,1))
plot(0:50, dgeom(0:50, prob=0.1), col='red4', type='p', pch=16, cex=1, xlab='x', ylab='p(x)', cex.lab=2, cex.axis=2
```

<img src="Lecture 3.assets/Screenshot 2025-11-28 at 12.33.25 AM.png" alt="Screenshot 2025-11-28 at 12.33.25 AM" style="zoom:50%;" />

#### Geometric distribution cdf

```R
par(mar=c(6,8,5,1))
plot(stepfun(0:50, c(0, pgeom(0:50, prob=0.1))), pch = 1, lwd=2, col='steelblue', xlab='x', ylab='F(x)', cex.lab=2, cex.axis=2, m
```

<img src="Lecture 3.assets/Screenshot 2025-11-28 at 12.33.09 AM.png" alt="Screenshot 2025-11-28 at 12.33.09 AM" style="zoom:50%;" />
