# Week 5 – Expectation, variance, and transformations of RVs

## Last class

* **Continuous random variables:**
    * Take infinite uncountable values
    * Have a probability density function (pdf)
    * Continuous RV are completely characterized by their pdf or cdf

* **Uniform:** $U[a,b]$
* **Exponential:** $Exp[\lambda]$
* **Normal:** $N(\mu,\sigma)$
* **Pareto:** $Pareto(x_{m},\alpha)$

* **Mixtures of distributions:**
    * Discrete + Discrete = Discrete
    * Continuous + Continuous = Continuous
    * Discrete + Continuous = Neither discrete nor continuous

For a continuous random variable, it follows from the definition of pdf and the fundamental theorem of calculus that for $a \le b$:

$$
P(a<X\le b) = \int_{a}^{b}f_{X}(t)dt = F_{X}(x)|_{a}^{b} = F(b)-F(a)
$$

But $P(a<X\le b)=F(b)-F(a)$ is true for any random variable (discrete, continuous or mixed):
Let $A=\{X\le a\}, B=\{X\le b\}$. Clearly, $A\subset B$ and $B-A=\{a<X\le b\}$.

$$
P(a<X\le b) = P(B-A) = P(B)-P(A) = P(X\le b)-P(X\le a) = F(b)-F(a)
$$

For a continuous RV (but not for a discrete or mixed) this also equals $P(a\le X\le b), P(a<X<b), \dots$

## Expectation for discrete RVs

The expected value is a weighted average of the values a random variable takes, weighted by the probability of taking those values. It's the center of 'gravity' where the distribution 'balances'.

For a **Discrete** random variable $X$, $f_{X}(x)$ the probability mass function of $X$, and $\{x_{1},x_{2},\dots\}$ is the support of $X$.

$$
E[X]=\sum_{x_{i}\in \text{supp}(X)}x_{i}f_{X}(x_{i})
$$

The support of a discrete random variable $X$ is the set of points that $X$ takes with non-zero probability:
$$
\text{supp}(X)=\{x_{i}:P(X=x_{i})>0\}
$$

## Expectation discrete examples: Bernoulli

Bernoulli trial, $X \sim \text{Bernoulli}(p)$

$$
X=\begin{cases}1&p\\ 0&1-p\end{cases}
$$

$f_{X}(0)=p$

$f_{X}(1)=1-p \quad (0\le p\le1)$

$$
E[X]=0\times(1-p)+1\times p=p
$$

## Expectation discrete examples: Binomial

$X \sim \text{Binomial}(n, p)$; models the number of successes in $n$ trials

$$
f_{X}(k)=\binom{n}{k}p^{k}(1-p)^{n-k} \quad k=0,1,\dots,n
$$

$$
E[X]=\sum_{k=0}^{n}k\binom{n}{k}p^{k}(1-p)^{n-k}=\sum_{k=1}^{n}k\binom{n}{k}p^{k}(1-p)^{n-k}= \\
=\sum_{k=1}^{n}k\frac{n!}{(n-k)!k!}p^{k}(1-p)^{n-k}=np\sum_{k=1}^{n}\frac{(n-1)!}{(n-k)!(k-1)!}p^{k-1}(1-p)^{n-k}= \\
=np\sum_{k=1}^{n}\binom{n-1}{k-1}p^{k-1}(1-p)^{n-k}=np\sum_{j=0}^{n-1}\binom{n-1}{j}p^{j}(1-p)^{n-1-j}= \\
=np(p+(1-p))^{n-1}=np
$$

## Expectation discrete examples: Poisson

A discrete random variable $X$ is said to have a $\text{Poisson}(\lambda)$ distribution with parameter $\lambda>0$ if 

$$
P(X=k)=\frac{e^{-\lambda}\lambda^{k}}{k!}
$$

for $k=0, 1, 2, \dots$



Used to model number of events happening in a period of time e.g. number of mutations per unit length in a DNA strand, number of new patients (incidence rates), number of phone calls/particles arriving in a system, etc.

<img src="Lecture 5.assets/Screenshot 2025-11-28 at 12.58.37 AM.png" alt="Screenshot 2025-11-28 at 12.58.37 AM" style="zoom:50%;" />

## Expectation examples: Poisson (contd)

$$
E[X]=\sum_{k=0}^{\infty}kf_{X}(k)=\sum_{k=0}^{\infty}k\frac{e^{-\lambda}\lambda^{k}}{k!}=\sum_{k=1}^{\infty}k\frac{e^{-\lambda}\lambda^{k}}{k!}= \\
=\lambda e^{-\lambda}\sum_{k=1}^{\infty}\frac{\lambda^{k-1}}{(k-1)!}=\lambda e^{-\lambda}\sum_{j=0}^{\infty}\frac{\lambda^{j}}{j!}= \\
=\lambda e^{-\lambda}e^{\lambda}=\lambda
$$

## Expectation for continuous RVs

For a **Continuous** random variable $X$, with $f_{X}(x)$ the probability density function of $X$, the expectation is defined as:

$$
E[X]=\int_{-\infty}^{+\infty}xf_{X}(x)dx
$$

NOTE: Expectation may not exist E.g. Cauchy distribution
$$
f(x)=\frac{1}{\pi(1+x^{2})}, \quad -\infty<x<+\infty
$$

## Expectation examples: continuous with finite support

$X \sim F(x)$

CDF:
$$
F(x)=\begin{cases}0&if~x<0\\ 2x^{2}-x^{4}&if~0\le x\le1\\ 1&if~x\ge1\end{cases}
$$

PDF:
$$
f(x)=F^{\prime}(x)=\begin{cases}4x-4x^{3}&if~0\le x\le1\\ 0&otherwise\end{cases}
$$

Expectation Calculation:
$$
E[X]=\int_{-\infty}^{+\infty}xf(x)dx=\int_{0}^{1}x(4x-4x^{3})dx=4\left(\frac{x^{3}}{3}-\frac{x^{5}}{5}\right)\bigg|_{0}^{1}=\frac{8}{15}
$$

## Expectation examples: continuous with infinite support

$X \sim \text{Exp}[\lambda]$, $f(x)=\lambda e^{-\lambda x}$ for $x\ge0$

$$
E[X]=\int_{-\infty}^{+\infty}xf(x)dx=\int_{0}^{+\infty}x\lambda e^{-\lambda x}dx=\frac{1}{\lambda}\int_{0}^{+\infty}te^{-t}dt
$$

(Using $t=\lambda x, dt=\lambda dx)$

$$
E[X]=\frac{1}{\lambda}\int_{0}^{+\infty}te^{-t}dt=\frac{1}{\lambda}\left(-te^{-t}\bigg|_{0}^{+\infty}-\int_{0}^{+\infty}e^{-t}dt\right)=\frac{1}{\lambda}(-e^{-t})\bigg|_{0}^{+\infty}=\frac{1}{\lambda}
$$

(integrating by parts)

## Expectation for a mixed random variable

For a mixed random variable $X$ with cdf $F(x)=pF_{1}(x)+(1-p)F_{2}(x)$ with $F_{1}$ continuous and $F_{2}$ discrete:

$$
E[X]=p\int_{-\infty}^{+\infty}xf_{1}(x)dx+(1-p)\sum_{x_{i}}x_{i}f_{2}(x_{i})
$$

where $f_{1}(x)$ is the density for the continuous component, $f_{1}(x)=F_{1}^{\prime}(x)$, and $f_{2}(x)$ is the mass function for the discrete component.

## Probabilities as expectations

For a set $A \subset \Omega$ the random variable:

$$
I_{A}(\omega)=\begin{cases}1&\omega\in A\\ 0&\omega\notin A\end{cases}
$$

is called the indicator function of the set $A$.

What is the distribution of $I_{A}$?

$I_{A} \sim \text{Bernoulli}(p), p=P(A) \Rightarrow E[I_{A}]=P(A)$

Allows us to work with random variables (indicator functions) instead of sets and expectations instead of probabilities

Exercise: If $A,B \subset \Omega$, what are $I_{A}I_{B}, \min(I_{A},I_{B}), \max(I_{A},I_{B})$?

## Transformations of random variables

Example: $X \sim F(x)$

$$
F(x)=\begin{cases}0&if~x<0\\ 2x^{2}-x^{4}&if~0\le x\le1\\ 1&if~x\ge1\end{cases}
$$

What is the cdf of $Y=-\sqrt{X+1}$ ?

First, $0\le X\le1 \iff -\sqrt{2}\le-\sqrt{X+1}\le-1$

## Transformations of random variables

For $-\sqrt{2}\le y\le-1$

$$
F_{Y}(y)=P(Y\le y)= \\
=P(-\sqrt{X+1}\le y)= \\
=P(-y\le\sqrt{X+1})= \\
=P(y^{2}-1\le X)= \\
=1-P(X<y^{2}-1)=1-P(X\le y^{2}-1)= \\
=1-F_{X}(y^{2}-1)=1-2(y^{2}-1)^{2}+(y^{2}-1)^{4}
$$

Final CDF:
$$
F_{Y}(y)=\begin{cases}0&if~y<-1\\ 1-2(y^{2}-1)^{2}+(y^{2}-1)^{4}&if~-\sqrt{2}\le y\le-1\\ 1&if~y>-\sqrt{2}\end{cases}
$$

## Change-of-variable formula for the expectation

Continuous $X$:

$$
E[g(X)]=\int_{-\infty}^{+\infty}g(x)f_{X}(x)dx
$$

Discrete $X$:

$$
E[g(X)]=\sum_{x_{i}}g(x_{i})f_{X}(x_{i})
$$

Allows us to compute the expectation of $Y=g(X)$ without deriving the pdf or pmf of $g(X)!!$

## Change-of-variable formula example

In the previous example computing $E[Y]=\int_{-\sqrt{2}}^{-1}yf_{Y}(y)dy$ seems to require knowing/deriving $f_{Y}(y)=F_{Y}^{\prime}(y)$ and integrating using the pdf of $Y$ (a big mess)

The change-of-variable formula allows us to use a shortcut:
$$
E[g(X)]=\int_{-\infty}^{+\infty}g(x)f_{X}(x)dx
$$

Only require us to integrate using the pdf of $X$!
$$
E[-\sqrt{X+1}]=\int_{0}^{1}-(\sqrt{x+1})(2x^{2}-x^{4})dx
$$

Using Mathematica: `Integrate[-Sqrt[(1+x)](2x^2-x^4), {x, 0, 1}]`

$$
E[-\sqrt{X+1}]=-\frac{4}{693}(103\sqrt{2}-40)
$$

## Variance

$$
Var[X]=E[(X-E[X])^{2}]=E[X^{2}]-E[X]^{2}
$$

$Var[X]$ is the average squared deviation from the mean. Measure of dispersion/concentration.

Continuous $X$:
$$
E[X^{2}]=\int_{-\infty}^{+\infty}x^{2}f_{X}(x)dx
$$

Discrete $X$:
$$
E[X^{2}]=\sum_{x_{i}}x_{i}^{2}f_{X}(x_{i})
$$