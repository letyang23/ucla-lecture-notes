# Week 10 – Maximum Likelihood Estimation

### Review - Unbiased Estimators

$X_{1}, \dots, X_{n}$ a random sample from distribution $F$, and a parameter of interest about $F$ (e.g. mean)

* An estimator $T$ of a parameter $\theta$ is **unbiased** if $E[T]=\theta$
* An unbiased estimator has no systematic tendency to produce estimates that are larger than or smaller than the target parameter $\theta$
* $\overline{X_{n}}$ is an unbiased estimator of the population mean $\mu$.
* $S_{n}^{2}=\frac{1}{n-1}\sum_{i=1}^{n}(X_{i}-\overline{X_{n}})^{2}$ is an unbiased estimator of the population variance $\sigma^{2}$
* Unbiasedness is not preserved under transformations.

### Last Class- Choosing among unbiased estimators. Example

* $X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} U[0, \theta]$
* $f_{X}(x) = \frac{1}{\theta}I_{[0,\theta]}(x)$
* $E[X_{i}] = \frac{\theta}{2}$, so $E[\overline{X_{n}}] = \frac{\theta}{2}$
* Then $\widetilde{\theta} = 2\overline{X_{n}}$ is an unbiased estimator for $\theta$

Intuitively a natural estimator for $\theta$ would also be based on $T = \max\{X_{1}, \dots, X_{n}\}$

* $f_{T}(t) = n\frac{t^{n-1}}{\theta^{n}}I_{[0,\theta]}(t)$
* $E[T] = \frac{n}{n+1}\theta$ so $\widehat{\theta} = \frac{n+1}{n}T$ is an unbiased estimator of $\theta$

So, both $\widetilde{\theta}$ and $\widehat{\theta}$ are unbiased estimators of $\theta$, which one is better?

### Last Class - Choosing among unbiased estimators-Example

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.50.08 PM.png" alt="Screenshot 2025-11-30 at 10.50.08 PM" style="zoom:50%;" />

### Last Class - Choosing among unbiased estimators example.

* We see empirically that $\widetilde{\theta}$ is much less variable than $\widehat{\theta}$
* But also theoretically, $Var[\widetilde{\theta}]=\frac{\theta^{2}}{n(n+2)}$ and $Var[\widehat{\theta}]=\frac{\theta^{2}}{3n}$
* So, $Var[\widetilde{\theta}]<Var[\widehat{\theta}]$ for $n\ge2$ and goes much faster to zero!
* Additionally, $\widehat{\theta}$ can take values way over the true $\theta$
* So, $\widetilde{\theta}$ is a much better estimate of $\theta$ than $\widehat{\theta}$

### Last Class- Mean square error

* Although **unbiasedness** is a desirable property, unbiased estimators do not always exist
* Even when they exist, requiring unbiasedness maybe too stringent (i.e. there can be other good estimators that are biased)
* A general performance of an estimator can be judged by the way it spreads around the parameter to be estimated:
  * If $T$ is an estimator for a parameter $\theta$, the **mean squared error** of $T$ is the number:
    $$MSE(T)=E[(T-\theta)^{2}]$$


* It's easy to show that $MSE(T)=Var(T)+Bias(T)^{2}$ where $Bias(T)=E[T]-\theta$
* A **biased estimator** with a small bias could be more useful than an **unbiased estimator** with a large variance.
* Better to use $MSE(T)$ to choose between estimators
* When $Bias(T)=0$, $MSE(T)=Var(T)$

### Last Class- Mean square error example

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} Poisson(\mu)$

Two candidate estimators for $p_{0}=P(X_{i}=0)=e^{-\mu}$:
* $\widetilde{p}_{0}=\frac{\text{number of } X_{i}=0}{n}$
* $\widehat{p}_{0}=e^{-\overline{X_{n}}}$

$\widetilde{p}_{0}$ is unbiased but $\widehat{p}_{0}$ is not? Which one is better?

### Last Class - Mean square error example

Simulation to see how the two estimators behave

* True $p_{0}=e^{-2} \approx 0.135$

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.52.13 PM.png" alt="Screenshot 2025-11-30 at 10.52.13 PM" style="zoom:50%;" />

### Last Class - Mean square error example

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.52.42 PM.png" alt="Screenshot 2025-11-30 at 10.52.42 PM" style="zoom:50%;" />

### Maximum likelihood estimation

Previous examples of estimators were sample analogs of population parameters (e.g. sample mean and sample variance) or intuitive (e.g. estimator based on $\max\{X_{1}, \dots, X_{n}\}$ for $U[0, \theta]$)

Maximum likelihood provides a very general way to construct estimators with good properties. The idea is intuitive:

* Choose as the estimator the value of $\theta$ that **maximizes the chances to produce the observed data.**

Example: An infusion pump is a medical device that delivers fluids - typically medications, nutrients, or saline - into a patient's body in controlled amounts over time. We track time to failure (in hours) for five identical infusion pumps used in a hospital.

* Observed data in hours: $120, 85, 200, 60, 150$
* Assuming independent and identically distributed lifetimes following an **$Exponential(\lambda)$ model.**
* Compute the maximum likelihood estimate of $\lambda$.

### MLE - exponential example

Data: $t_{1}=120$, $t_{2}=85$, $t_{3}=200$, $t_{4}=60$, $t_{5}=150$

Model: i.i.d data with density $f(t|\lambda)=\lambda e^{-\lambda t}$

Likelihood:

$$L(\lambda)=\prod_{i=1}^{5}\lambda e^{-\lambda T_{i}}$$
$$=(\lambda e^{-\lambda\cdot120})(\lambda e^{-\lambda\cdot85})(\lambda e^{-\lambda\cdot200})(\lambda e^{-\lambda\cdot60})(\lambda e^{-\lambda\cdot150})$$
$$=\lambda^{5}exp[-\lambda(120+85+200+60+150)]=\lambda^{5}exp(-615\lambda)$$

log-likelihood:

$$l(\lambda)=log~L(\lambda)=5~log~\lambda-615~\lambda$$

### MLE - exponential example

Setting the score to zero to find the candidate maxima of the log-likelihood:

$$\frac{dl}{d\lambda}=\frac{5}{\lambda}-615$$

$$\frac{5}{\lambda}-615=0\Rightarrow\hat{\lambda}=\frac{5}{615}=0.00813$$

Checking $2^{nd}$ derivative:

$$\frac{d^{2}l}{d\lambda^{2}}=-\frac{5}{\lambda^{2}}<0$$

### Maximum likelihood estimation – exponential example

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.55.34 PM.png" alt="Screenshot 2025-11-30 at 10.55.34 PM" style="zoom:50%;" />

### Maximum likelihood estimation - exponential example

Let $T_{1}, \dots, T_{n} \stackrel{i.i.d}{\sim} Exp(\lambda)$ with density $f(t;\lambda)=\lambda e^{-\lambda t}$ for $t>0$. The likelihood and log-likelihood are

$$L(\lambda)=\prod_{i=1}^{n}\lambda e^{-\lambda T_{i}}=\lambda^{n}exp\left(-\lambda\sum_{i=1}^{n}T_{i}\right)$$

$$l(\lambda)=\log L(\lambda)=n\log\lambda-\lambda\sum_{i=1}^{n}T_{i}$$

Differentiate and set to zero:

$$\frac{dl}{d\lambda}=\frac{n}{\lambda}-\sum_{i=1}^{n}T_{i}=0 \Rightarrow \hat{\lambda}=\frac{n}{\sum_{i=1}^{n}T_{i}}$$

### MLE - a more complex example Number of cycles until pregnancy:

Number of cycles until pregnancy:

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.56.42 PM.png" alt="Screenshot 2025-11-30 at 10.56.42 PM" style="zoom:50%;" />

### MLE - a more complex example

* Want to estimate $p=P(X=1)$, where $X_{i}$ is the number of cycles up to pregnancy among the $i^{th}$ smoker
* We know that $S=\frac{\text{number of } X_{i}=1}{n}$ is an unbiased estimator for $p$
* This yields the estimate $\widetilde{p}=\frac{29}{100}=0.29$
* But it uses only a fraction of the data discarding the rest. Maybe there is a better estimator using all the data?

### MLE - a more complex example

* Let $X_{i}$ denote the number of cycles up to pregnancy for the $i^{th}$ smoker. We can assume the $X_{i} \sim Geometric(p)$, and the $X_{i}$ are independent. There are 415 smokers

* The probability of observing the data in the first row of the table is then given by:

  $$L(p)=P(X_{1}=x_{1}|p)\times P(X_{2}=x_{2}|p)\times\dots P(X_{100}=x_{100}|p)$$

  $$=p^{29}\cdot(p(1-p))^{16}\dots((1-p)^{11}p)^{3}\cdot((1-p)^{12})^{7}$$

  $$=p^{93}(1-p)^{322}$$

* We want to find $0\le p\le1$ that makes $L(p)$ as large as possible, i.e. find the value of $p$ that maximizes $L(p)$
* Equivalent to finding the maximizer of $l(p)=\log(L(p))$

### MLE - a more complex example

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.59.55 PM.png" alt="Screenshot 2025-11-30 at 10.59.55 PM" style="zoom:50%;" />

$$l(p)=93\log(p)+322\log(1-p)$$

$$0=l^{\prime}(p)=\frac{93}{p}-\frac{322}{1-p}\iff p=\frac{93}{415}$$

$$\hat{p}=\frac{93}{415}=0.224$$ is called the maximum likelihood estimate of $p$.

### Maximum likelihood estimation

* The **maximum likelihood estimate** of $\theta$ is the value $\hat{\theta}=\hat{\theta}(x_{1}, x_{2}, \dots, x_{n})$ that maximizes the log-likelihood function $l(\theta)$.
* The corresponding random variable $\hat{\theta}=\hat{\theta}(X_{1}, X_{2}, \dots, X_{n})$ is called the **maximum likelihood estimator** of $\theta$.
* (We often use the same notation, $\hat{\theta}$ for both the estimate and the estimator. We understand which one we are referring to based on context)

### MLE with no analytical solution

Dataset: $x_{1}, \dots, x_{n}$ modeled as a realization of random variables $X_{1}, \dots, X_{n}.$

Where the pdf of $X_{i}$ is a mixture of exponentials:

$X_{i} \sim Exp(\lambda)$ with probability $\frac{1}{2}$ and $Exp(2\lambda)$ with probability $\frac{1}{2}$

$$f(x)=\frac{1}{2}\lambda e^{-\lambda x}+\frac{1}{2}2\lambda e^{-2\lambda x}$$

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 11.01.00 PM.png" alt="Screenshot 2025-11-30 at 11.01.00 PM" style="zoom:50%;" />

### MLE with no analytical solution

```r
set.seed(101)
n = 50

rate = 1
mix = rbinom(n=n, size=1, prob=1/2)
dataset = mix*rexp(n, rate=rate) + (1-mix)*rexp(n, rate=2*rate)

negloglik = function(x, data) {
    -sum(log(0.5*dexp(data, rate=x) + 0.5*dexp(data, rate=2*x)))
}

optimize(f=negloglik, interval=c(0.01, 10), data=dataset)

## $minimum
## [1] 1.37906

## $objective
## [1] 19.78651
```

### MLE with no analytical solution

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 11.01.00 PM.png" alt="Screenshot 2025-11-30 at 11.01.00 PM" style="zoom:50%;" />

### Properties of Maximum likelihood estimators

The maximum likelihood estimator (MLE) is **consistent**:
$$\hat{\theta}_{n} \stackrel{P}{\longrightarrow} \theta \text{ as } n\rightarrow+\infty.$$

* i.e. as the sample size gets larger the MLE gets closer and closer to the true parameter $\theta$.
* Consistency is much stronger that asymptotic unbiasedness.

**Invariance:**

* If $\hat{\theta}$ is the MLE of $\theta$ then $g(\hat{\theta})$ is the MLE of $g(\theta)$.

**Asymptotic minimum variance**

* No other consistent estimator has lower asymptotic mean squared error.

**Asymptotic normality**
* In most situations of interest (but not always, e.g. $U[0, \theta]$) the sampling distribution of the MLE gets closer and closer to a **normal distribution** as $n\rightarrow\infty$.

With few exceptions MLE's are generally **biased estimators**.

### Asymptotic variance of the MLE

Let $X_{1}, \dots, X_{n} \sim f(x;\theta)$ and the log-likelihood function: $l(\theta)=\sum_{i=1}^{n}\log f(X_{i};\theta)$

The **Fisher's information** of $\theta$ (for one sample) is defined as:

$$
I(\theta)=-E\left[\frac{\partial^{2}l(\theta,X)}{\partial\theta^{2}}\right]
$$

If $f(x;\theta)$ is 'well behaved' (e.g. its support does not depend on $\theta$)


$$
\sqrt{n}(\hat{\theta}-\theta) \stackrel{d}{\longrightarrow} N\left(0, \frac{1}{I(\theta)}\right)
$$

* $\frac{1}{nI(\theta)}$ is the asymptotic variance of $\hat{\theta}$

The standard error of the MLE is $se(\hat{\theta})=\frac{1}{\sqrt{nI(\theta)}}$

We can estimate the standard error of the MLE by $\widehat{se}(\hat{\theta})=\frac{1}{\sqrt{nI(\hat{\theta})}}$

