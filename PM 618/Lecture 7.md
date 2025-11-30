# Week 7 – Transformation of RVs, Law of large numbers

### Last Class 

- Random vector = multiple random variables defined on the same probability space. 
- Discrete (have joint pmf) and continuous (have joint pdf) random vectors.
- LOTUS to compute the expectation of a transformed random vector. 
- Independence of random variables. 
- Covariance and correlation.

### Distribution of a sum of discrete RVs

(X, Y) a random vector. What is the distribution of $Z=X+Y$?

* If (X, Y) is discrete then
    $$
    P_{Z}(z)=\sum_{x_{i}+y_{i}=z}P_{X,Y}(x_{i},y_{i})
    $$

* Example: Let X and Y be independent random variables with common pmf given by
    $P_{X}(0)=\frac{1}{4}$, $P_{X}(1)=\frac{1}{2}$, $P_{X}(2)=\frac{1}{4}$. Find the pmf of $Z=X+Y$.

### Distribution of a sum of continuous RVs

(X, Y) a random vector and $Z=X+Y$

If (X, Y) is continuous then
$$f_{Z}(z)=\int_{-\infty}^{+\infty}f_{X,Y}(x,z-x)dx=\int_{-\infty}^{+\infty}f_{X,Y}(z-y,y)dy$$

Example: $X\sim Exp(\lambda)$, $Y\sim U[0,1]$, X and Y independent. Find the cdf and the pdf of $Z=X+Y$.

### Bivariate normal distribution

Two random variables X and Y are said to have a **bivariate normal distribution** if their joint pdf is given by:

$$f_{XY}(x,y)=\frac{1}{2\pi\sigma_{X}\sigma_{Y}\sqrt{1-\rho^{2}}}\cdot exp\{-\frac{1}{2(1-\rho^{2})}[(\frac{x-\mu_{X}}{\sigma_{X}})^{2}+(\frac{y-\mu_{Y}}{\sigma_{Y}})^{2}-2\rho\frac{(x-\mu_{X})(y-\mu_{Y})}{\sigma_{X}\sigma_{Y}}]\}$$

$$\mu=\begin{pmatrix}\mu_{X}\\ \mu_{Y}\end{pmatrix}=E\begin{pmatrix}X\\ Y\end{pmatrix}$$ and

$$\Sigma=\begin{pmatrix}Var(X)&Cov(X,Y)\\ Cov(X,Y)&Var(Y)\end{pmatrix}=\begin{pmatrix}\sigma_{X}^{2}&\rho\sigma_{X}\sigma_{Y}\\ \rho\sigma_{X}\sigma_{Y}&\sigma_{Y}^{2}\end{pmatrix}$$ is the variance-covariance-matrix.

where $\rho\in(-1,1),\sigma_{X}>0,\sigma_{Y}>0$.

$$(X,Y)\sim N(\mu,\Sigma)$$

### Sums of normals

* If $X\sim N(\mu_{X},\sigma_{X}^{2})$, $Y\sim N(\mu_{Y},\sigma_{Y}^{2})$ are **independent** then
    $$X+Y\sim N(\mu_{X}+\mu_{Y},\sigma_{X}^{2}+\sigma_{Y}^{2})$$

* If $(X,Y)\sim N(\mu,\Sigma)$ then
    $$X+Y\sim N(\mu_{X}+\mu_{Y},\sigma_{X}^{2}+\sigma_{Y}^{2}+2\rho\sigma_{X}\sigma_{Y})$$

* If $X\sim N(\mu_{X},\sigma_{X}^{2}),Y\sim N(\mu_{Y},\sigma_{Y}^{2})$ but not bivariate normal then $X+Y$ are not necessarily normal.

* Example: $X\sim N(\mu,\sigma^{2}),Y=-X$. $Y\sim N(-\mu,\sigma^{2})$ but $X+Y=0$, a constant random variable.

### Sum of independent exponentials

$X_{1},...,X_{n}\stackrel{iid}{\sim}Exp(\lambda)$ then $Z=X_{1}+...+X_{n}\sim Gamma(n,\lambda)$

A continuous random variable has a **gamma distribution** with parameters $\alpha>0$ and $\lambda>0$ if its probability density function is given by:

$$f(x)=\frac{\lambda(\lambda x)^{\alpha-1}e^{-\lambda x}}{\Gamma(\alpha)}I_{[0,+\infty)}(x)$$

where

$$\Gamma(\alpha)=\int_{0}^{+\infty}t^{\alpha-1}e^{-t}dt$$

for $\alpha>0$ is the **gamma function**.

The gamma function is a generalization of the factorial: $\Gamma[\alpha+1]=\alpha\Gamma[\alpha]$ and $\Gamma[n+1]=n!$ for $n=0,1,2,...$

### Maximum and minimum

$X_{1},...,X_{n}\sim F(x)$ iid random variables and $U=min(X_{1},...,X_{n}),$
$V=max(X_{1},...,X_{n})$

Then:

$$F_{V}(v)=F(v)^{n}$$

(if continuous with density $f(x)$, then $f_{V}(v)=nf(v)F(v)^{n-1}$

$$F_{U}(u)=1-(1-F(u))^{n}$$

(if continuous with density $f(x)$ then $f_{U}(u)=nf(u)(1-F(u))^{n-1}$

### Averaging reduces variability

$X_{1},X_{2}\sim F(x)$ independent

$Var(X_{1})=Var(X_{2})=\sigma^{2}$

$$Var(\frac{X_{1}+X_{2}}{2})=\frac{1}{2^{2}}(Var(X_{1})+Var(X_{2}))=\frac{1}{2^{2}}(\sigma^{2}+\sigma^{2})=\frac{\sigma^{2}}{2}$$

### Averaging reduces variability

$X_{1},X_{2},...$ i.i.d with expectation $\mu$ and variance $\sigma^{2}$

$$\overline{X_{n}}=\frac{X_{1}+...+X_{n}}{n}$$

$$E[\overline{X_{n}}]=\frac{1}{n}(E[X_{1}]+...+E[X_{n}])=\frac{1}{n}\underbrace{(\mu+...+\mu)}_{n~times}=\mu$$

$$Var[\overline{X_{n}}]=\frac{1}{n^{2}}(Var[X_{1}]+...+Var[X_{n}])=\frac{1}{n^{2}}\underbrace{(\sigma^{2}+...+\sigma^{2})}_{n~times}=\frac{\sigma^{2}}{n}$$

### Markov's inequality

If $U\ge0$ is a random variable with finite expectation, then, for every $t>0$:

$$P(U\ge t)\le\frac{E[U]}{t}$$

Intuition:

* Let U be the income of a random selected individual from a population. Taking $t=2E[U]$, Markov's inequality says that $P(U\ge2E[U])\le\frac{1}{2}$. It is impossible for more than half of the population to make at least twice the average income.

* This has to be true because if more than half of the population make more than twice the average income, the average income would have to be higher!

* Taking $t=3E[U]$, we get $P(U\ge3E[U])\le\frac{1}{3}$. It is impossible for more than one third of the population to make at least 3 times the average income.

##### Proof

$U\ge0$ a random variable with finite expectation, $t>0$:

Define the new random variable $U_{t}=\begin{cases}0&if~U<t\\ t&if~U\ge t\end{cases}$

$U_{t}$ is discrete random variable taking only values 0 and t. So, $E[U_{t}]=tP(U\ge t).$

Clearly $U\ge U_{t}$

Expectations preserve inequalities, so, $E[U]\ge E[U_{t}]\Rightarrow E[U]\ge tP(U\ge t)\Rightarrow P(U\ge t)\le\frac{E[U]}{t}$

### Chebyshev's inequality

If X is a random variable with mean $\mu$ and variance $\sigma^{2}$ , then, for every $t>0$:

* $$P(|X-E[X]|\ge t)\le\frac{Var[X]}{t^{2}}$$

or equivalently

* $$P(|X-E[X]|<t)\ge1-\frac{Var[X]}{t^{2}}$$

or equivalently

* $$P(\frac{|X-E[X]|}{\sigma}\ge t)\le\frac{1}{t^{2}}$$

#### Proof

X a random variable with mean $\mu$ and variance $\sigma^{2}$, $t>0$

Consider the non-negative random variable $U=(X-\mu)^{2}$

Apply Markov's inequality to U, with $t^{2}:P(U\ge t^{2})=P((X-\mu)^{2}\ge t^{2})\le\frac{E[(X-\mu)^{2}]}{t^{2}}=\frac{Var(X)}{t^{2}}$

Noticing that $\{|X-\mu|\ge t\}=\{(X-\mu)^{2}\ge t^{2}\}$, we get Chebyshev's inequality:

$$P(|X-\mu|\ge t)\le\frac{Var(X)}{t^{2}}$$

### Chebyshev's inequality consequences

Any random variable with finite variance (continuous, discrete, mixed), regardless of its distribution, has most of its probability mass concentrated within a few standard deviations of its mean.

Taking $t=k\sigma, k=2,3,4$ and applying Chebishev's inequality:

$$P(|X-E[X]|\ge k\sigma)\le\frac{\sigma^{2}}{k^{2}\sigma^{2}}=\frac{1}{k^{2}}$$

$$P(|X-E[X]|\le k\sigma)\ge1-\frac{1}{k^{2}}$$

For $k=2,3,4$ the bound are $3/4$, $8/9$, and $15/16$ respectively

### Weak Law of large numbers (WLLN)

$X_{1},X_{2},...$ i.i.d with finite expectation $\mu$ then:

$$\lim_{n\rightarrow\infty}P(|\overline{X_{n}}-\mu|>\epsilon)=0$$

This form of convergence of random variables is called **convergence in probability** and is denoted as
$$\overline{X_{n}}\stackrel{P}{\rightarrow}\mu$$

Equivalently:

$$\lim_{n\rightarrow\infty}P(|\overline{X_{n}}-\mu|\le\epsilon)=1$$

**The sample mean converges to the true mean**

### (Weak) Law of large numbers

##### Proof

$X_{1},X_{2},...$ i.i.d with finite expectation $\mu$.

To make the proof easier, we will also assume that $\sigma^{2}<+\infty$

But the for the WLLN to hold only the expectation needs to exist. The variance may be infinite.

Let $\epsilon>0$. Apply Chebyshev's inequality to $\overline{X_{n}}:$

$$P(|\overline{X_{n}}-\mu|\ge\epsilon)\le\frac{Var(\overline{X_{n}})}{\epsilon^{2}}=\frac{\sigma^{2}}{n\epsilon^{2}}$$

This implies:

$$\lim_{n\rightarrow\infty}P(|\overline{X_{n}}-\mu|\ge\epsilon)=0$$

### Strong Law of large numbers (SLLN)

$X_{1},X_{2},...$ i.i.d with finite expectation $\mu$.

$$P(\lim_{n\rightarrow\infty}\overline{X_{n}}=\mu)=1$$

This form of convergence of random variables is called **convergence with probability 1** and is denoted as
$$\overline{X_{n}}\stackrel{w.p.1}{\longrightarrow}\mu$$
(also called **almost sure convergence**)

The strong law is **stronger** than weak law because convergence with probability 1 is a stronger concept
than convergence in probability: convergence with probability $1\implies$ convergence in probability (but not the other way around)

### Law of large numbers

$X_{1},X_{2},...,X_{n}\sim N(1,1)$

Five realizations of $\overline{X_{n}}$ as a function of $n$

<img src="Lecture 7.assets/image-20251129161727499.png" alt="image-20251129161727499" style="zoom:50%;" />

