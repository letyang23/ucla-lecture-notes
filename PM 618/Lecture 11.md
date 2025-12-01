# Week 11 – Confidence Intervals

### Last Class - Maximum Likelihood

Maximum likelihood is a general method for estimating parameters of interest

Idea: choose parameter the maximizes the probability of observing the data actually observed

* The probability of observing the data actually observed as a function of parameter = **likelihood**
* Previous examples of estimators were sample analogs of population parameters (e.g. sample mean and sample variance) or intuitive (e.g. estimator based on $\max_{1\le i\le n}X_{i}$ for $U[0,\theta]$)

Maximum likelihood can be used in cases when there is no 'natural' estimator like sample mean or variance

### Maximum likelihood estimation

* The **maximum likelihood estimate** of $\theta$ is the value $\hat{\theta}=\hat{\theta}(x_{1},x_{2}, \dots, x_{n})$ that maximizes the log-likelihood function $l(\theta)$.
* The corresponding random variable $\hat{\theta}=\hat{\theta}(X_{1},X_{2}, \dots, X_{n})$ is called the **maximum likelihood estimator** of $\theta$.
* (We often use the same notation, $\hat{\theta}$ for both the estimate and the estimator. We understand which one we are referring to based on context)

### Properties of Maximum likelihood estimators

The **maximum likelihood estimator (MLE) is consistent**:
$$\hat{\theta}_{n}\rightarrow\theta \text{ as } n\rightarrow+\infty$$

* i.e. as the sample size gets larger the MLE gets closer and closer to the true parameter $\theta$.
* Consistency is **stronger than asymptotic unbiasedness** (which MLEs also have)

**Invariance**:
* If $\hat{\theta}$ is the MLE of $\theta$ then $g(\hat{\theta})$ is the MLE of $g(\theta)$.
* E.g. MLE of $\theta^{2}$ is $\hat{\theta}^{2}$

**Asymptotic minimum variance**
* Lowest asymptotic mean squared error.

**Asymptotic normality**
* The distribution of the MLE gets closer and closer to a **normal distribution** as $n\rightarrow\infty$.

* MLE's are generally **biased estimators** - But bias disappears as sample size increases (asymptotically unbiased).

### Asymptotic variance of the MLE

Let $X_{1}, \dots, X_{n}\sim f(x;\theta)$ and the log-likelihood function: $l(\theta)=\sum_{i=1}^{n}\log f(X_{i};\theta)$

The **Fisher's information** of $\theta$ (for one sample) is defined as:

$$
I(\theta)=-E\left[\frac{\partial^{2}l(\theta,X)}{\partial\theta^{2}}\right]
$$

If $f(x;\theta)$ is 'well behaved' (e.g. its support does not depend on $\theta$):
$$
\sqrt{n}(\hat{\theta}-\theta) \stackrel{d}{\longrightarrow} N\left(0, \frac{1}{I(\theta)}\right)
$$
* $\frac{1}{nI(\theta)}$ is the asymptotic variance of $\hat{\theta}$


The standard error of the MLE is $se(\hat{\theta})=\frac{1}{\sqrt{nI(\theta)}}$

We can estimate the standard error of the MLE by $\widehat{se}(\hat{\theta})=\frac{1}{\sqrt{nI(\hat{\theta})}}$

### Confidence intervals

So far we've considered what are called **point estimators**.

* A point estimator by itself not that useful; need some measure of how variable the estimator is
* To supplement point estimators with information about their variability we can also report their SD, called the **standard error (SE)**
* A better option is to report a whole interval of plausible values for the parameter of interest, i.e. a **confidence interval**.

Based on Chebysheb's inequality, if $T$ is an estimator for $\theta$, and $\sigma_{T}$ is the standard deviation of $T$:

$$P(|T-\theta|\ge2\sigma_{T})\le\frac{3}{4}$$

$$P(\theta\in(T-2\sigma_{T},T+2\sigma_{T}))\ge\frac{3}{4}$$

$(T-2\sigma_{T},T+2\sigma_{T})$ is an **interval estimator** for $\theta$

### Confidence intervals

* Dataset $x_{1}, \dots, x_{n}$ modeled as a realization of random variables $X_{1}, \dots, X_{n}.$
* $\theta$ the parameter of interest (e.g. mean, variance, probability, etc.), and $0<\alpha<1$
* A $(1-\alpha)$-level interval estimator for $\theta$ is a a pair of sample statistics $L_{n}=g(X_{1}, \dots, X_{n})$ and $U_{n}=h(X_{1}, \dots, X_{n})$ such that:
  * $$P(L_{n}<\theta<U_{n})=1-\alpha \text{ for every value of } \theta$$


* The interval $(l_{n}, u_{n})$ where $l_{n}=g(x_{1}, \dots, x_{n})$ and $u_{n}=h(x_{1}, \dots, x_{n}),$ is called a $100(1-\alpha)\%$ **confidence interval** for $\theta$.
* The number $\alpha$ is called the **confidence level**.
* Often, we only require $P(L_{n}<\theta<U_{n})>1-\alpha$ or $P(L_{n}<\theta<U_{n})\approx1-\alpha$
  * These are **conservative** and **approximate** interval estimators respectively

### Interval estimator for the normal mean - variance known

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} N(\mu, \sigma^{2})$, with $\sigma^{2}$ known. We want to construct an interval estimator for $\mu$.

* $\overline{X_{n}}$ is an unbiased estimator for $\mu$. It is also consistent and it's the MLE (with all its properties)
* We know that $\frac{\overline{X_{n}}-\mu}{\sigma/\sqrt{n}}\sim N(0,1)$
* Then, $$P\left(-z_{\alpha/2}\le\frac{\overline{X_{n}}-\mu}{\sigma/\sqrt{n}}\le z_{\alpha/2}\right)=1-\alpha$$
* Equivalently, $$P\left(\mu\in\left(\overline{X_{n}}-z_{\alpha/2}\frac{\sigma}{\sqrt{n}},\overline{X_{n}}+z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right)\right)=1-\alpha$$
* $\left(\overline{x_{n}}-z_{\alpha/2}\frac{\sigma}{\sqrt{n}},\overline{x_{n}}+z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right)$ is a $100(1-\alpha)\%$ confidence interval for $\mu$
* Common confidence levels are $95\%$ and $99\%$

### Interval estimator for the normal mean - variance known

One hundred $95\%$ confidence intervals for $\mu=7.7$

<img src="Lecture 11.assets/Screenshot 2025-11-30 at 11.12.41 PM.png" alt="Screenshot 2025-11-30 at 11.12.41 PM" style="zoom:50%;" />

### Confidence interval for the normal mean - variance unknown

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} N(\mu, \sigma^{2})$ with $\sigma^{2}$ unknown. We want an interval estimator for $\mu$.

* In most situations the $\sigma^{2}$ is not known, so we cannot use the interval estimator above
* Idea: estimate $\sigma^{2}$ by the sample variance $S_{n}^{2}$ (and $\sigma$ by $S_{n}$)
* $\frac{\overline{X_{n}}-\mu}{S_{n}/\sqrt{n}}$ is not normal; it has a **t-distribution $n-1$ degrees of freedom**, $t(n-1)$
* The pdf of a $t(n)$ distribution is $$f(x)=k_{n}\left(1+\frac{x^{2}}{n}\right)^{-\frac{n+1}{2}}$$ for $-\infty<x<+\infty$, where $k_{n}$ is a constant.

### t-distribution

<img src="Lecture 11.assets/Screenshot 2025-11-30 at 11.13.16 PM.png" alt="Screenshot 2025-11-30 at 11.13.16 PM" style="zoom:50%;" />

### Confidence interval for the normal mean - variance unknown

We know that $\frac{\overline{X_{n}}-\mu}{S_{n}/\sqrt{n}}\sim t(n-1)$

So, $$P\left(\mu\in\left(\overline{X_{n}}-t_{n-1,\alpha/2}\frac{S_{n}}{\sqrt{n}},\overline{X_{n}}+t_{n-1,\alpha/2}\frac{S_{n}}{\sqrt{n}}\right)\right)=1-\alpha$$

$$\left(\overline{x_{n}}-t_{n-1,\alpha/2}\frac{S_{n}}{\sqrt{n}},\overline{x_{n}}+t_{n-1,\alpha/2}\frac{S_{n}}{\sqrt{n}}\right) \text{ is a } 100(1-\alpha)\% \text{ confidence interval for } \mu$$

### Asymptotic interval estimator for the mean

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} F$ with $E[X_{i}]=\mu$. We want an interval estimator for $\mu$.

* Now we don't know the distribution of $X_{i}$ (it could be normal or anything else)
* The CLT states that: $\frac{\sqrt{n}(\overline{X_{n}}-\mu)}{\sigma}\stackrel{D}{\longrightarrow} N(0,1)$
* A variant of the CLT applies if we replace $\sigma$ with the estimate $S_{n}$: $\frac{\sqrt{n}(\overline{X_{n}}-\mu)}{S_{n}}\stackrel{D}{\longrightarrow} N(0,1)$
* So, $$P\left(\mu\in\left(\overline{X_{n}}-z_{\alpha/2}\frac{S_{n}}{\sqrt{n}},\overline{X_{n}}+z_{\alpha/2}\frac{S_{n}}{\sqrt{n}}\right)\right)\approx1-\alpha$$
* $\left(\overline{X_{n}}-z_{\alpha/2}\frac{S_{n}}{\sqrt{n}},\overline{X_{n}}+z_{\alpha/2}\frac{S_{n}}{\sqrt{n}}\right)$ is an **approximate** $100(1-\alpha)\%$ interval estimator for $\mu$

### Confidence interval for the mean - example

Let $x_{1}, \dots, x_{n}$ be a dataset modeled as a realization of i.i.d random variables $X_{1}, \dots, X_{n}$ with $E[X_{i}] = \mu$

Which interval for $\mu$ would you choose in each of these scenarios?

* $X_{i} \sim N(\mu, 2)$
* $X_{i} \sim N(\mu, \sigma^{2})$
* $X_{i} \sim F$

### Confidence interval for a proportion

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} Bernoulli(p)$ or equivalently $X=X_{1}+\dots+X_{n} \sim Binomial(n,p)$

* $\hat{p}=\overline{X_{n}}=\frac{X}{n}$ is the MLE of $p$
* $Var(\hat{p})=\frac{p(1-p)}{n}$; $SD(\hat{p})=\sqrt{\frac{p(1-p)}{n}}$
* A natural estimator of $SD(\hat{p})$ is $\hat{se}(\hat{p})=\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}$; standard error of $\hat{p}$
* By the CLT we have $$\frac{\sqrt{n}(\hat{p}-p)}{\sqrt{p(1-p)}}\approx N(0,1)$$
* By a variant of the CLT we have $$\frac{\sqrt{n}(\hat{p}-p)}{\sqrt{\hat{p}(1-\hat{p})}}\approx N(0,1)$$
* So, $$\left(\hat{p}-z_{\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}},\hat{p}+z_{\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}\right)$$ is an approximate $100(1-\alpha)\%$ interval estimator for $p$
* Can also write as: $(\hat{p}-z_{\alpha/2}\hat{se}(\hat{p}), \hat{p}+z_{\alpha/2}\hat{se}(\hat{p}))$

### Confidence interval for a proportion

Example: $n=1,000$ poll showed that 557 voters intend to vote for candidate A and 443 for candidate B.

$p$ proportion of all voters that intend to vote for A
$\hat{p}=557/1000=0.557=55.7\%$

$\hat{se}(\hat{p})=\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}=\sqrt{0.557(1-0.557)/1000)}=0.0157$

$95\% \text{ CI for } p$: $(\hat{p}-1.96\times\hat{se}(\hat{p}), \hat{p}+1.96\times\hat{se}(\hat{p}))=(0.526,0.588)$

Margin of error $=1.96\times\hat{se}(\hat{p})=0.03$

"This poll is accurate to plus or minus $3\%$ points 19 times out of 20"

### Asymptotic variance of the MLE

Let $X_{1}, \dots, X_{n} \sim f(x;\theta)$ and the log-likelihood function: $l(\theta)=\sum_{i=1}^{n}\log f(X_{i};\theta)$

The **Fisher's information** of $\theta$ (for one observation) is defined as:
$$I_{1}(\theta)=-E\left[\frac{\partial^{2}l_{1}(\theta,X)}{\partial\theta^{2}}\right]$$

where $l_{1}(\theta)=\log f(X;\theta)$ is the log-likelihood for one observation

If $f(x;\theta)$ is 'well behaved' (e.g. its support does not depend on $\theta$)

* $$\sqrt{n}(\hat{\theta}-\theta) \stackrel{d}{\longrightarrow} N\left(0, \frac{1}{I_{1}(\theta)}\right)$$
* $\frac{1}{nI_{1}(\theta)}$ is the asymptotic variance of $\hat{\theta}$
* The standard error of the MLE is $se(\hat{\theta})=\frac{1}{\sqrt{nI_{1}(\theta)}}$
* We can estimate the standard error of the MLE by $\widehat{se}(\hat{\theta})=\frac{1}{\sqrt{nI_{1}(\hat{\theta})}}$

### Asymptotic confidence intervals based on MLES

Estimate of the standard error (i.e. $sd(\hat{\theta}))$:
$$\hat{se}(\hat{\theta})=\frac{1}{\sqrt{nI_{1}(\hat{\theta})}}$$

Based on the asymptotic normality of the MLE an approximate $100(1-\alpha)\%$ confidence interval can be computed as:
$$\left(\hat{\theta}-z_{\alpha/2}\hat{se}(\hat{\theta}), \hat{\theta}+z_{\alpha/2}\hat{se}(\hat{\theta})\right)=\left(\hat{\theta}-\frac{z_{\alpha/2}}{\sqrt{nI_{1}(\hat{\theta})}}, \hat{\theta}+\frac{z_{\alpha/2}}{\sqrt{nI_{1}(\hat{\theta})}}\right)$$

### Asymptotic confidence intervals based on MLES

Example: $X_{1}, \dots, X_{n} \sim Geometric(p)$; $P(X=x)=p(1-p)^{x-1}$

$$L(p)=\prod_{i=1}^{n}p(1-p)^{x_{i}-1}=p^{n}(1-p)^{\sum_{i=1}^{n}X_{i}-n}$$

$$l(p)=n\log(p)+\left(\sum_{i=1}^{n}X_{i}-n\right)\log(1-p)$$

$$l^{\prime}(p)=\frac{n}{p}-\frac{\sum_{i=1}^{n}X_{i}-n}{1-p}=0 \implies p=\frac{n}{\sum_{i=1}^{n}X_{i}}=\frac{1}{\overline{X}_{n}}$$

So, MLE of $p$ is $\hat{p}=\frac{1}{\overline{X}_{n}}$

### Asymptotic confidence intervals based on MLES

```r
set.seed(1909)
nsims = 100; n = 70; p = 0.3
p_hat = replicate(nsims, {X = rgeom(n, p) + 1; 1/mean(X)})
```

<img src="Lecture 11.assets/Screenshot 2025-11-30 at 11.17.12 PM.png" alt="Screenshot 2025-11-30 at 11.17.12 PM" style="zoom:50%;" />

### Asymptotic confidence intervals based on MLEs

$l_{1}^{\prime\prime}(p) = -\frac{1}{p^{2}} - \frac{X-1}{(1-p)^{2}}$ ($l_{1}(p)$ is log-likelihood for a single observation $X$)

Fisher information for one observation:
$$I_{1}(p) = -E[l_{1}^{\prime\prime}(p)] = \frac{1}{p^{2}} + \frac{\frac{1}{p}-1}{(1-p)^{2}} = \frac{1}{p^{2}(1-p)}$$

$$se(\widehat{p}) = \sqrt{(nI_{1}(p))^{-1}} = \frac{p\sqrt{1-p}}{\sqrt{n}}$$

$$\widehat{se}(\widehat{p}) = \frac{\widehat{p}\sqrt{1-\widehat{p}}}{\sqrt{n}}$$

$$\left( \widehat{p} - z_{\alpha/2}\frac{\widehat{p}\sqrt{1-\widehat{p}}}{\sqrt{n}}, \widehat{p} + z_{\alpha/2}\frac{\widehat{p}\sqrt{1-\widehat{p}}}{\sqrt{n}} \right)$$

### Asymptotic confidence intervals based on MLEs

Example $X_{1}, \dots, X_{70} \sim Geometric(p), \overline{X} = 3.714$

$\widehat{p} = 0.269$

$$\widehat{se}(\widehat{p}) = \frac{\widehat{p}\sqrt{1-\widehat{p}}}{\sqrt{70}} = 0.0275$$

$$\left( \widehat{p} - z_{\alpha/2}\widehat{se}(\widehat{p}), \widehat{p} + z_{\alpha/2}\widehat{se}(\widehat{p}) \right) =$$

$$= (0.269 - 1.96 \times 0.0275, \quad 0.269 + 1.96 \times 0.0275) = (0.220, 0.318)$$