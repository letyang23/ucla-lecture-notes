# Week 9 – Unbiased estimation - Efficiency, MSE

### Last Class-CLT

$X_{1},...,X_{n}\stackrel{i.i.d.}{\sim}X$ $E[X_{i}]=\mu,Var[X_{i}]=\sigma^{2}$ then:

Sum form: $S_{n}=X_{1}+...+X_{n}$

$$
Z_{n}=\frac{S_{n}-E[S_{n}]}{\sqrt{Var[S_{n}]}}=\frac{S_{n}-n\mu}{\sqrt{n}\sigma}\stackrel{D}{\rightarrow}N(0,1)
$$

Sample mean form: $$\overline{X_{n}}=\frac{X_{1}+...+X_{n}}{n}$$

$$
Z_{n}=\frac{\overline{X_{n}}-E[\overline{X_{n}}]}{\sqrt{Var[\overline{X_{n}}]}}=\frac{\sqrt{n}(\overline{X_{n}}-\mu)}{\sigma}\stackrel{D}{\rightarrow}N(0,1)
$$

The symbol $\stackrel{D}{\rightarrow}$ denotes **convergence in distribution**. It means that as $n\rightarrow\infty$ the cumulative distribution function of $Z_{n}=\frac{S_{n}-n\mu}{\sqrt{n}\sigma}=\frac{\sqrt{n}(\overline{X_{n}}-\mu)}{\sigma}$ gets closer and closer to the cdf of a standard normal.

Formally, if $F_{n}(x)=F_{Z_{n}}(x)$ denotes the cdf of $Z_{n}$, then $F_{n}(x)\rightarrow\Phi(x)$ for every $x\in\mathbb{R}$, where $\Phi(x)$ is the cdf of a $N(0,1)$ RV.

### Last Class-Basic statistical model

- Want to learn characteristics of a population:

  - Income of Los Angeles residents

  * Blood pressure of patients from LA county hospital

  * Vaping among teenagers in California

  * Genotypes at a gene among individuals with Hispanic ancestry


* We model the distribution of the characteristic as a random variable X (e.g. height, blood pressure, vaping (yes vs. no), Genotypes (0,1,2))

* To learn about X we collect a random sample: $X_{1},X_{2},...,X_{n}$ from $F_{X}(x),$ the distribution of X

* $X_{1},X_{2},...,X_{n}$ have the same probability distribution and are mutually independent.

* The distribution $F_{X}(x)$ of $X_{i}$ is unknown or only partially known.

* E.g. $X_{i}\sim N(\mu,\sigma^{2})$ with known $\sigma^{2}$ but unknown $\mu$

### Estimation

- We want to learn about a distribution in a population

* e.g. proportion of democrat voters in CA, average blood pressure among covid survivors aged $70+$, vaping frequency among young adults in the US, rate of patient ER night admissions in LA county hospitals

* We take a sample of size $n$ from the population and conceptualize it as a random sample $X_{1},...,X_{n}$ from a distribution $F_{X}(x)$ that is **totally or partially unknown to us.**

* We want to estimate specific characteristics or **parameters** of the underlying distribution:
    * true mean $E[X_{i}]=\mu$ (e.g. blood pressure)
    * the true variance, $Var[X_{i}]=\sigma^{2}$ (e.g. blood pressure)
    * or a probability like $P(X_{i}=1)$ (e.g. $X_{i}=1$ if democrat voter; $0=$ if not democrat voter)
    * or a rate (e.g. expected number of ER patients per hour) ($X_{i}=$ number of patients within a period of 1-hour)

---

Example 1: To estimate the unknown mean of a population $\mu$ (e.g. blood pressure)

- Natural to use the **sample mean** $\overline{X_{n}}$ to estimate $\mu$ because we know that for large $n$ the sample mean will be close to the true mean.

Example 2. We can model the number of arrivals per hour at an ER unit as a $Poisson(\lambda)$. Suppose we count the arrivals during each on $n$ (non-overlapping) 1-hour intervals to get the random sample $X_{1},...,X_{n}$. Here $\lambda$ is unknown and we want to estimate it.

- A natural estimate is also the **sample mean** $\overline{X_{n}}$ because $E[X_{i}]=\lambda$

- But using the **sample variance** $S_{n}^{2}$ is also reasonable because $Var[X_{i}]=\lambda$

- Today we'll learn how to choose among different options for estimating a parameter of interest

### Estimator vs. estimate

* **Estimate**: value t that only depends on the dataset $x_{1},x_{2},...,x_{n},$ i.e., t is some function of the dataset $t=h(x_{1},x_{2},...,x_{n})$. Example: $t=\overline{x_{n}}=\frac{x_{1}+...+x_{n}}{n}$

* An **estimate** is a number (or a vector of numbers in more complex problems)

* **Estimator**: Let $t=h(x_{1},x_{2},...,x_{n})$ be an estimate based on the dataset $x_{1},x_{2},...,x_{n}$. Then t is a realization of the random variable $T=h(X_{1},X_{2},...,X_{n})$. The random variable $T$ is called an estimator.

* An **estimator** is a random variable

* An **estimate** is a realization of random variable

### Sampling distribution

Example: estimating the proportion $p$ of LA teenagers that vape from a sample $X_{1},...X_{n}$
$X_{i}\sim Bernoulli(p)$.

$X_{i}$ records whether the teenager vapes (yes=1 vs. no=0)

* The sample proportion $\hat{p}_{n}=\frac{S_{n}}{n}$ of vapers is a natural estimator of $p$ ($S_{n}=X_{1}+...+X_{n}$ is the total number of vapers in the sample), because by the LLN $\hat{p}{\rightarrow}p$

* The **sampling distribution** is just the standard distribution (pdf, pmf, cdf) of the random variable we call the **estimator**.

* For example of vapers, the sampling distribution of $\hat{p}_{n}$ is the distribution of the random variable $$\hat{p}_{n}=\frac{S_{n}}{n}$$

### Sampling distribution of the sample proportion

Simulating one study: $X_{1},...,X_{n}\sim Bernoulli(p)$

```R
set.seed (2023)
$n=200$ # sample size
$p=0.35$ # True population frequency (eg. vaping among teenagers)
$x=$ rbinom(n, size $=1$, prob=p)
mean (x)

## [1] 0.37
```

### Sampling distribution of the sample proportion

Simulating MULTIPLE studies

```R
for (i in 1:nsims){
    X = rbinom(n, size = 1, prob=p)
    p_hat[i] = mean(X)
}
```

<img src="Lecture 9.assets/image-20251129163933199.png" alt="image-20251129163933199" style="zoom:67%;" />

### Sampling distribution of the sample mean

Simulating one study: $X_{1},...,X_{n}\sim Pareto(x_{m},\alpha)$

```r
library(EnvStats)
set.seed(2023)

n = 200 # sample size

loc = 10; alpha = 2 # E[X_i] = 20; e.g. income distribution in $1000
x = rpareto(n, location = loc, shape=alpha)
mean(x)

## [1] 21.14341
```

```r
for (i in 1:nsims) {
    x = rpareto(n, location = loc, shape=alpha)
    mu_hat[i] = mean(x)
}
```

<img src="Lecture 9.assets/image-20251129164115939.png" alt="image-20251129164115939" style="zoom:80%;" />