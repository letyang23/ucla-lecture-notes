# Week 8 – Central Limit Theorem

### Last Class

* **Markov's inequality:** for any RV $U\ge0$
    $$P(U\ge t)\le\frac{E[U]}{t} \quad for~any~t>0$$

* **Chebyshev's inequality:** for any RV $X, Var[X_{i}]<\infty;$
    $$P(|X-E[X]|\ge t)\le\frac{Var[X]}{t^{2}} \quad for~any~t>0$$

* **Law of large numbers:** $X_{1},X_{2},...$ i.i.d with finite expectation $\mu$:
    * **Weak:** $$\lim_{n\rightarrow\infty}P(|\overline{X}_{n}-\mu|>\epsilon)=0$$
    * **Strong:** $$P(\lim_{n\rightarrow\infty}\overline{X}_{n}=\mu)=1$$

### Basic Statistical Model

- Want to learn characteristics of a population:

  * Income of Los Angeles residents

  * Blood pressure of patients form LA county hospital

  * Vaping in among teenagers in California

  * Genotypes at a gene among individuals with Hispanic ancestry


* We model the distribution of the characteristic as a random variable X (e.g. height, blood pressure, vaping (yes vs. no), Genotypes (0,1,2)))
* To learn about X we collect a random sample: $X_{1},X_{2},...,X_{n}$ from $F_{X}(x)$ the distribution of X
* $X_{1},X_{2},...,X_{n}$ have the same probability distribution and are mutually independent.
* The distribution $F(x;\theta)$ of $X_{i}$ is unknown or only partially known
    * E.g. $X_{i}\sim N(\mu,\sigma^{2})$ with known $\sigma^{2}$ but unknown $\mu$
* We conceptualize the observed data $x_{1},...,x_{n}$ as realizations of the random variables $X_{1},...,X_{n}$

### Sample statistics

Sample statistics are empirical summaries of the data:

* sample mean: $$\overline{x}_{n}=\frac{x_{1}+...+x_{n}}{n}$$

* sample variance: $$s_{n}^{2}=\frac{1}{n-1}\sum_{i=1}^{n}(x_{i}-\overline{x}_{n})^{2}$$(sometimes$$\frac{1}{n}\sum_{i=1}^{n}(x_{i}-\overline{x}_{n})^{2})$$

* sample minimum: $$x_{(1)}=min(x_{1},...,x_{n})$$

We think of these as realizations of the corresponding random variables:

$$\overline{X_{n}}=\frac{X_{1}+...+X_{n}}{n}$$

$$S_{n}^{2}=\frac{1}{n-1}\sum_{i=1}^{n}(X_{i}-\overline{X_{n}})^{2}$$

$$X_{(1)}=min(X_{1},...,X_{n})$$

### Central Limit Theorem

$X_{1},...,X_{n}$ i.i.d. $E[X_{i}]=\mu, Var[X_{i}]=\sigma^{2}$ then:

Sum form: $S_{n}=X_{1}+...+X_{n}$

$$Z_{n}=\frac{S_{n}-E[S_{n}]}{\sqrt{Var[S_{n}]}}=\frac{S_{n}-n\mu}{\sqrt{n}\sigma}\stackrel{D}{\rightarrow}N(0,1)$$

Sample mean form: $$\overline{X_{n}}=\frac{X_{1}+...+X_{n}}{n}$$

$$Z_{n}=\frac{\overline{X}_{n}-E[\overline{X}_{n}]}{\sqrt{Var[\overline{X}_{n}]}}=\frac{\sqrt{n}(\overline{X}_{n}-\mu)}{\sigma}\stackrel{D}{\rightarrow}N(0,1)$$

The symbol $\stackrel{D}{\rightarrow}$ denotes **convergence in distribution**. It means that as $n\rightarrow\infty$ the cumulative distribution function of $Z_{n}=\frac{S_{n}-n\mu}{\sqrt{n}\sigma}=\frac{\sqrt{n}(\overline{X}_{n}-\mu)}{\sigma}$ gets closer and closer to the cdf of a standard normal.

Formally, if $F_{n}(x)=F_{Z_{n}}(x)$ denotes the cdf of $Z_{n}$, then $F_{n}(x)\rightarrow\Phi(x)$ for every $x\in\mathbb{R}$, where $\Phi(x)$ is the cdf of a $N(0,1)$ RV.

---

Sum of n i.i.d. exponentials: $S_{n}=X_{1}+...+X_{n}, X_{i}\sim Exp(2)$

<img src="Lecture 8.assets/image-20251129162125105.png" alt="image-20251129162125105" style="zoom:80%;" />

Blue line is pdf of $S_{n}$. Red line is pdf of a normal $N(\frac{n}{2},\frac{n}{4})$

### Example

A runner attempts to pace a 100m race. Her strides (steps) are independently distributed with mean $\mu=0.97$ meters and a standard deviation of $\sigma=0.1$. What is the (approximate) probability that her 100 strides differ from 100 meters by no more than five meters?

### Estimation

We want to learn about a distribution in a population

* e.g. proportion of democrat voters in CA, average blood pressure among covid survivors aged $70+$, vaping frequency among young adults in the US, rate of patient ER night admissions in LA county hospitals

* We take a sample of size $n$ from the population and conceptualize it as a random sample $X_{1},...,X_{n}$ from a distribution $F_{X}(x)$ that is **totally or partially unknown to us**.

* We want to estimate specific characteristics or **parameters** of the underlying distribution:
    * true mean $E[X_{i}]=\mu$ (e.g. $X_{i}$ blood pressure)
    * the true variance, $Var[X_{i}]=\sigma^{2}$ (e.g. $X_{i}$ blood pressure)
    * or a probability like $P(X_{i}=1)$ (e.g. $1=$ democrat voter; $0=$ not democrat voter)
    * or a rate (e.g. expected number of ER patients per hour) ($X_{i}=$ number of patients within a period of $1$-hour)

---

Example 1: To estimate the unknown mean of a population $\mu$ (e.g. blood pressure)

- Natural to use the **sample mean** $\overline{X}_{n}$ to estimate $\mu$ because we know that for large $n$ the sample mean will be close to the true mean.

Example 2. We can model the number of arrivals per hour at an ER unit as a $Poisson(\lambda)$. Suppose we count the arrivals during each on $n$ (non-overlapping) 1-hour intervals to get the random sample $X_{1},...,X_{n}$. Here $\lambda$ is unknown and we want to estimate it.

- A natural estimate is also the **sample mean** $\overline{X}_{n}$ because $E[X_{i}]=\lambda$.

- But using the **sample variance** $S_{n}^{2}$ is also reasonable because $Var[X_{i}]=\lambda$

- In future classes we'll learn how to choose among different options for estimating a parameter of interest

### Estimator vs. estimate

* Estimate: value t that only depends on the dataset $x_{1},x_{2},...,x_{n},$ i.e., t is some function of the dataset $t=h(x_{1},x_{2},...,x_{n}).$ Example: $t=\overline{x}_{n}=\frac{x_{1}+...+x_{n}}{n}$

* An *estimate is a number* (or a vector of numbers in multi-parameter estimation problems)

* **Estimator**: Let $t=h(x_{1},x_{2},...,x_{n})$ be an estimate based on the dataset $x_{1},x_{2},...,x_{n}$. Then $t$ is a realization of the random variable $T=h(X_{1},X_{2},...,X_{n})$. The random variable T is called an estimator.

* *An estimator is a random variable*

* *An estimate is a realization of random variable*

### Sampling distribution

Example: estimating the proportion $p$ of LA teenagers that vape from a sample $Y_{1},...Y_{n}$
$Y_{i}\sim Bernoulli(p)$.

- $Y_{i}$ records whether the teenager vapes (yes=1 vs. no=0)

* The sample proportion $\hat{p}_{n}=\frac{S_{n}}{n}$ of vapers is a natural estimator of $p$ ($S_{n}=Y_{1}+...+Y_{n}$ is the total number of vapers in the sample), because by the LLN $\hat{p}_{n}{\rightarrow}p$

* The sampling distribution is just the standard distribution (pdf, pmf, cdf) of the random variable we call the estimator.

* For example of vapers, the sampling distribution of $\hat{p}_{n}$ is the distribution of the random variable $$\hat{p}_{n}=\frac{S_{n}}{n}$$

### Unbiased Estimators

$X_{1},...X_{n}$ a random sample from distribution F, and $\theta$ a parameter of interest about F (e.g. mean)

* An estimator $T$ of a parameter $\theta$ is unbiased if $E[T]=\theta$

* An unbiased estimator has no systematic tendency to produce estimates that are larger than or smaller than the target parameter $\theta$

* The difference $E[T]-\theta$ is called the bias of the estimator $T$

* If $bias\ne0$ the estimator is called biased

### Sample Mean and sample variance

- $X_{1},...X_{n}$ a random sample with mean $E[X_{i}]=\mu$ and $Var[X_{i}]=\sigma^{2}$

* The sample mean $\overline{X}_{n}$ is an unbiased estimator of the population mean $\mu$.
    $$E[\overline{X}_{n}]=\mu$$

* The sample variance $S_{n}^{2}=\frac{1}{n-1}\sum_{i=1}^{n}(X_{i}-\overline{X}_{n})^{2}$ is an unbiased estimator of the population variance $\sigma^{2}$
    $$E[S_{n}^{2}]=\sigma^{2}$$

### Unbiasedness is not preserved under general transformations

* In general, if $T$ is an unbiased estimator of $\theta$, $g(T)$ is not an unbiased estimate of $g(\theta)$
* Example:
    * $\overline{X}_{n}$ is unbiased for $E[X_{i}]=\mu$
    * But $\overline{X}_{n}^{2}$ is not unbiased for $E[X_{i}]^{2}=\mu^{2}$, Because by Jensen's inequality $E[\overline{X}_{n}^{2}]>E[\overline{X}_{n}]^{2}=\mu^{2}$
* **Jensen's inequality:** if $g(t)$ is a convex function, then $E[g(T)]\ge g(E[T])$. Equality holds only if $g(x)=at+b$
* If $g$ linear $g(t)=at+b, E[g(T)]=E[aT+b]=aE[T]+b=g(E[T])$ so $g(T)$ is unbiased for $g(\theta)$
