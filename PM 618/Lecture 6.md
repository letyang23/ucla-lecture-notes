# Week 6 – Random vectors and independence

## Last class

**Expectation**

* **Continuous:**
    $$E[X]=\int_{-\infty}^{+\infty}xf_{X}(x)dx$$
* **Discrete:**
    $$E[X]=\sum_{x_{i}}x_{i}f_{X}(x_{i})$$
* **Mixed:**
    $$E[X]=w_{d}\sum_{x_{i}}x_{i}f_{X}(x_{i})+w_{c}\int_{-\infty}^{+\infty}xf_{X}(x)dx; \quad w_{d}+w_{c}=1$$

**Variance**

* $$Var[X]=E[(X-E[X])^{2}]=E[X^{2}]-E^{2}[X]$$

**Change of variable formula/LOTUS**

* **Continuous:**
    $$E[g(X)]=\int_{-\infty}^{+\infty}g(x)f_{X}(x)dx$$
* **Discrete:**
    $$E[g(X)]=\sum_{x_{i}}g(x_{i})P_{X}(x_{i})$$

## Random vectors

We are typically interested in not one, but multiple related random variables defined on the same space.

* $X, Y$ random variables or $(X, Y)$ a random vector in $\mathbb{R}^{2}$
    * E.g. weight and height of a randomly selected person
* Geometrically, $(X, Y)$ represents a random point in $\mathbb{R}^{2}$
* More generally, a random vector in $\mathbb{R}^{n}$, $\mathbf{X}=(X_{1},\dots,X_{n})$
    * E.g. expression levels of $n$ genes for an individuals
* We can have discrete, continuous, and mixed random vectors

## Discrete random vectors

A random vector $(X, Y)$ is discrete if it takes a finite or countable number of values
$R_{X,Y}=\{(x_{1},y_{1}),(x_{2},y_{2}),\dots\}$

Joint probability mass function:

* $$P_{X,Y}(x,y)=P(X=x,Y=y)=P(X=x\cap Y=y)$$

* $$P(X\in A\cap R_{X},Y\in B\cap R_{Y})=\sum_{x_{i}\in A}\sum_{y_{j}\in B}P_{X,Y}(x_{i},y_{j})$$

In general, if $C\subset\mathbb{R}^{2}$,

* $$P((X,Y)\in C)=\sum_{(x_{i},y_{j})\in C\cap R_{X,Y}}P_{X,Y}(x_{i},y_{j})$$

$X$ and $Y$ are discrete random variables $\iff (X,Y)$ is a discrete random vector

## Continuous random vectors

A random vector is continuous if it has a joint probability density function:

* $$f_{X,Y}(x,y)\ge0$$
* $$\iint_{\mathbb{R}^{2}}f_{X,Y}(x,y)dx~dy=1$$
* $$P((X,Y)\in C)=\iint_{C}f_{X,Y}(x,y)dx~dy$$

$(X, Y)$ continuous as a random vector $\Rightarrow X$ and $Y$ continuous as individual random variables

Converse is not true: $X$ and $Y$ are continuous $\not\Rightarrow (X,Y)$ continuous as a random vector (it may not have a density)

## Random vectors

The cumulative distribution function (cdf) is defined for both discrete and continuous (and mixture) random vectors:

$$
F_{XY}(x,y)=P(X\le x,Y\le y)=\begin{cases}\int_{-\infty}^{x}\int_{-\infty}^{y}f_{X,Y}(s,t)dsdt & \text{Continuous} \\ \sum_{x_{i}\le x}\sum_{y_{j}\le y}P_{X,Y}(x_{i},y_{j}) & \text{Discrete} \end{cases}
$$

Just like for random variables, the pdf (continuous), the pmf (discrete), or the cdf (both), completely characterize probabilistically a random vector

For a continuous random vector:
$$
f_{X,Y}(x,y)=\frac{\partial^{2}}{\partial x\partial y}F_{X,Y}(x,y)
$$

The distribution (pdf, pmf or cdf) of the component random variables $X$ and $Y$ are called the marginal distribution of $X$ and $Y$ respectively

## Marginal distributions

$(X, Y)$ a random vector

$$
F_{X}(x)=\lim_{y\rightarrow+\infty}F_{X,Y}(x,y) \quad F_{Y}(y)=\lim_{x\rightarrow+\infty}F_{X,Y}(x,y)
$$

For a continuous random vector:

$$
f_{X}(x)=\int_{-\infty}^{+\infty}f_{X,Y}(x,y)dy \quad f_{Y}(y)=\int_{-\infty}^{+\infty}f_{X,Y}(x,y)dx
$$

For a discrete random vector:

$$
P_{X}(x_{i})=\sum_{y_{j}}P_{X,Y}(x_{i},y_{j}) \quad P_{Y}(y_{j})=\sum_{y_{j}}P_{X,Y}(x_{i},y_{j})
$$

## Example: discrete random vector

Let $M$ and $S$ be the minimum and the sum of two independent rolls of fair 3-faced die.

Determine:

* The joint pmf of $M$ and $S$.
* The marginal pmf of $M$ and of $S$.

## Example: continuous random vector

Suppose that the joint cumulative distribution function of $(X, Y)$ is given by:

$$
F_{X,Y}(x,y)=\begin{cases}1-e^{-2x}-e^{-y}+e^{-(2x+y)}& \text{if } x>0, y>0 \\ 0& \text{Otherwise} \end{cases}
$$
<img src="Lecture 6.assets/Screenshot 2025-11-28 at 1.09.26 AM.png" alt="Screenshot 2025-11-28 at 1.09.26 AM" style="zoom:50%;" />

## Example: continuous random vector

$$
F_{X,Y}(x,y)=\begin{cases}1-e^{-2x}-e^{-y}+e^{-(2X+y)}& \text{if } x>0, y>0 \\ 0& \text{Otherwise} \end{cases}
$$

1. Determine the joint probability density function of $X$ and $Y$.
2. Determine the marginal cumulative distribution functions of $X$ and $Y$.
3. Determine the marginal probability density functions of $X$ and $Y$.
4. Find out whether $X$ and $Y$ are independent.
5. Determine $\text{Cov}(X,Y)$ and $\rho(X,Y)$

## Example: continuous random vector

Suppose that the joint probability density function of $X$ and $Y$ is given:

$$
f_{X,Y}(x,y)=\begin{cases}x+cy^{2}&if~0\le x\le1,0\le y\le1\\ 0&Otherwise\end{cases}
$$

1. Find the constant $c$.
2. Determine the joint cumulative distribution functions of $(X, Y)$.
3. Determine the marginal probability density functions of $X$ and $Y$.
4. Find out whether $X$ and $Y$ are independent.
5. Determine \text{Cov}(X,Y) and $\rho(X,Y)$

## Independence of random variables

$X$ and $Y$ are independent if for any $A, B \subset \mathbb{R}$, $\{X \in A\}$ and $\{Y \in B\}$ are independent events:
$$
P(X \in A, Y \in B) = P(X \in A)P(Y \in B)
$$

* Equivalent to the factorization of the joint cdf as a product of the marginal cdfs:
$$
F_{X,Y}(x,y) = F_{X}(x)F_{Y}(y)
$$

* For continuous random vectors, also equivalent to the factorization of the joint pdf as a product of the marginal pdfs:
$$
f_{X,Y}(x,y) = f_{X}(x)f_{Y}(y)
$$

* For discrete random vectors, also equivalent to the factorization of the joint pmf as a product of the marginal pmfs:
$$
P_{X,Y}(x,y) = P_{X}(x)P_{Y}(y)
$$

* Definition of independence and factorization equivalences extend to multiple random variables $X_{1}, \dots, X_{n}$

## Propagation of independence

NOTE this is important and not covered in the book

* If $X$, and $Y$ are independent so are $g(X)$ and $h(Y)$ for $g,h:\mathbb{R}\rightarrow\mathbb{R}$

* If $X_{1},X_{2},\dots,X_{n}$ are independent so are $h_{1}(X_{1}),\dots,h_{n}(X_{n}),$ for $h_{i}:\mathbb{R}\rightarrow\mathbb{R}$

* If $X_{1},\dots,X_{n},Y_{1},\dots,Y_{m}$ are independent then, $g(X_{1},\dots,X_{n}),h(Y_{1},\dots,Y_{m}),$ where $g:\mathbb{R}^{n}\rightarrow\mathbb{R},h:\mathbb{R}^{m}\rightarrow\mathbb{R}$

Examples:

1. $X_{1},X_{2},X_{3},X_{4},Y_{1},Y_{2}$ independent $\Rightarrow Z_{1}=\frac{\sin(X_{1}^{2})+e^{X_{2}}}{X_{3}^{5}+1},Z_{2}=\cos(Y_{1})-Y_{2}^{3}$ are independent

2. $X_{1},X_{2},\dots,X_{n}\stackrel{iid}{\sim} \text{Bernoulli}(p),$ $Y_{1},Y_{2},\dots,Y_{m}\stackrel{iid}{\sim} \text{Bernoulli}(q)$
(iid stands for independent identically distributed)

Let $X=X_{1}+X_{2}+\dots+X_{n}, Y=Y_{1}+Y_{2}+\dots+Y_{m}.$

Then $X\sim \text{Binomial}(n,p)$ and $Y\sim \text{Binomial}(m,q)$ and $X, Y$ are independent

## Expectation of a random vector

$$
E[(X,Y)]=(E[X],E[Y])
$$

Interpretation is analog to that for random variables, 'center' of the two-dimensional distribution, center of mass if we think of probability as mass distributed on the surface of the plane $\mathbb{R}^{2}$

In general,
$$
E[\mathbf{X}]=(E[X_{1}],\dots,E[X_{n}])
$$

Example: $X\sim \text{Exp}(\lambda_{1}), Y\sim \text{Exp}(\lambda_{2})$
$$
E[(X,Y)]=(E[X],E[Y])=\left(\frac{1}{\lambda_{1}},\frac{1}{\lambda_{2}}\right)
$$

## Multi-dimensional LOTUS

$\mathbf{X}=(X_{1},\dots,X_{n})$ a random vector, $g:\mathbb{R}^{n}\rightarrow\mathbb{R}$ a function, then:

$$
E[g(\mathbf{X})] = E[g(X_{1},\dots,X_{n})] = \begin{cases}\int_{\mathbb{R}^{n}}g(x_{1},\dots,x_{n})f_{\mathbf{X}}(x_{1},\dots,x_{n})dx_{1}\dots dx_{n} & \text{if } \mathbf{X} \text{ continuous} \\ \sum_{\mathbf{x}_{i}}g(\mathbf{x}_{i})f_{\mathbf{X}}(\mathbf{x}_{i}) & \text{if } \mathbf{X} \text{ discrete} \end{cases}
$$

Consequences:

* **Expectation is linear:**
$$
E[a_{1}X_{1}+a_{2}X_{2}+\dots+a_{n}X_{n}]=a_{1}E[X_{1}]+a_{2}E[X_{2}]+\dots+a_{n}E[X_{n}]
$$

* $$E[XY]=E[X]E[Y] \quad \text{for independent random variables } X, Y$$

Example of linearity: $X\sim \text{Binomial}(n,p)$

Then, $X=X_{1}+\dots+X_{n}$ where $X_{1},X_{2},\dots X_{n}\sim \text{Bernoulli}(p)$

$$
E[X]=E[X_{1}]+\dots+E[X_{n}]=\underbrace{p+\dots+p}_{\text{n times}}=np
$$

## Covariance

For arbitrary random variables $X$ and $Y$:

$$
Var[X+Y]=Var[X]+Var[Y]+2E[(X-E[X])(Y-E[Y])]
$$

The term:
$$
\text{Cov}(X,Y)=E[(X-E[X])(Y-E[Y])]=E[XY]-E[X]E[Y]
$$
is called the covariance of $X$ and $Y$.

It measures how much $X$ and $Y$ co-vary, i.e. vary together.

* $\text{Cov}(X,Y)>0$ if whenever $X>E[X]$ is likely that also $Y>E[Y]$ and vice versa (and that when $X<E[X]$ also more likely that $Y<E[Y]$)

* $\text{Cov}(X,Y)<0$ if whenever $X>E[X]$ is likely that $Y<E[Y]$ and vice versa (and that when $X<E[X]$ also more likely that $Y>E[Y]$)

* $X,Y$ independent $\Rightarrow \text{Cov}(X,Y)=0$

* Converse is not true: $\text{Cov}(X,Y)=0\Rightarrow X,Y$ independent

## Covariance

Example of additivity of variance for uncorrelated RVs

$X\sim \text{Binomial}(n,p)$

Then, $X=X_{1}+\dots+X_{n}$ where $X_{1},X_{2},\dots X_{n}\stackrel{iid}{\sim} \text{Bernoulli}(p)$

$$
Var[X]=Var[X_{1}]+\dots+Var[X_{n}]+\sum_{i<j}2\text{Cov}(X_{i},X_{j})= \\
=\underbrace{p(1-p)+\dots+p(1-p)}_{\text{n times}}=np(1-p)
$$

## Properties of covariance

* Covariance is linear in each of its terms:
$$
\text{Cov}(aX+bY,cU+dV)=ac\text{Cov}(X,U)+ad\text{Cov}(X,V)+bc\text{Cov}(Y,U)+bd\text{Cov}(Y,V)
$$

$$
\text{Cov}(X,X)=Var[X] \quad (\Rightarrow Var[aX]=a^{2}Var[X])
$$
* **Cauchy-Schwartz inequality**
$$
|E[XY]| \le \sqrt{E[X^{2}]E[Y^{2}]}
$$
* From Cauchy-Schwartz inequality using $X-E[X]$ and $Y-E[Y]$ in place of $X$ and $Y$, it follows that
$$
|\text{Cov}(X,Y)| \le \sqrt{Var[X]Var[Y]} = \sigma_{X}\sigma_{Y}
$$
($\sigma_{X}=\sqrt{Var[X]},\sigma_{Y}=\sqrt{Var[Y]}$ are called the standard deviations of $X$ and $Y$ respectively)

* Equivalently,
$$
-1\le\frac{\text{Cov}(X,Y)}{\sqrt{Var[X]Var[Y]}}\le1
$$

## Correlation

$$
\rho(X,Y)=\frac{\text{Cov}(X,Y)}{\sqrt{Var[X]Var[Y]}} \quad \text{is the correlation between } X \text{ and } Y
$$

* $X, Y \text{ independent } \Rightarrow \rho(X,Y)=0$

* Converse is not true: $\rho(X,Y)=0 \Rightarrow X, Y \text{ independent}$

* $\rho(X,Y)$ is a standardized version of $\text{Cov}(X,Y)$

* $\rho(X,Y)$ is unaffected by changes of units:
$$
\rho(aX+b, cY+d)=\rho(X,Y)
$$

* Covariance it's not invariant: $\text{Cov}(X,Y)=\rho(X,Y)\sigma_{X}\sigma_{Y}$, so the larger $\sigma_{X}$ and $\sigma_{Y}$, the larger $\text{Cov}(X,Y)$ in absolute value (provided $\rho(X,Y)\ne0$)