# Probability Review

### Bernoulli trials

**Definition**

A random variable is called **Bernoulli random variable** with parameter $p$ if its probability mass function is given by equation

$$
p(x)=\begin{cases}1-p=q & \text{if } x=0 \\ p & \text{if } x=1 \\ 0 & \text{otherwise}\end{cases} \quad p(x)=\begin{cases}p^{x}(1-p)^{1-x} & \text{if } x=0 \text{ or } 1 \\ 0 & \text{otherwise}\end{cases}
$$

For a Bernoulli random variable $X$ with parameter $p, 0 < p < 1$,

$$E(X)=p, \quad Var(X)=p(1-p)$$

### Example

If in a throw of a fair die the event of obtaining 4 or 6 is called a success, and the event of obtaining 1, 2, 3, or 5 is called a failure, then $X$ is a Bernoulli random variable. Determine its probability mass function, its expected value $E(X)$ and variance $Var(X)$.

**Solution:**

$$
X=\begin{cases}1 & \text{if 4 or 6 is obtained} \\ 0 & \text{otherwise}\end{cases}
$$

The parameter $p=1/3$. Therefore, its probability mass function is

$$
p(x)=\begin{cases}2/3 & \text{if } x=0 \\ 1/3 & \text{if } x=1 \\ 0 & \text{elsewhere.}\end{cases}
$$

$E(X)=p=1/3$, and $Var(X)=1/3(1-1/3)=2/9$.