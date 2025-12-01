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

### Choosing among unbiased estimators. Example

* $X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} U[0, \theta]$
* $f_{X}(x) = \frac{1}{\theta}I_{[0,\theta]}(x)$
* $E[X_{i}] = \frac{\theta}{2}$, so $E[\overline{X_{n}}] = \frac{\theta}{2}$
* Then $\widehat{\theta} = 2\overline{X_{n}}$ is an unbiased estimator of $\theta$

Intuitively a natural estimate for theta could also be based on $T = \max\{X_{1}, \dots, X_{n}\}$

* $f_{T}(t) = n\frac{t^{n-1}}{\theta^{n}}I_{[0,\theta]}(t)$
* $E[T] = \frac{n}{n+1}\theta$ so $\widetilde{\theta} = \frac{n+1}{n} T$ is an unbiased estimator of $\theta$

So, both $\widehat{\theta}$ and $\widetilde{\theta}$ are unbiased estimators of $\theta$, which one is better?

### Choosing among unbiased estimators-Example.

Let's perform a simulation to see how the two estimators behave:

```r
set.seed(101)
theta = 2
n = 50
nsims = 500
theta_hat = theta_tilde = numeric(nsims)

for (i in 1:nsims){
    x = runif(n=n, max=theta)
    theta_hat[i] = 2 * mean(x)
    theta_tilde[i] = ((n+1)/n) * max(x)
}
```

### Choosing among unbiased estimators-Example

<img src="Lecture 9.assets/Screenshot 2025-11-30 at 10.25.31 PM.png" alt="Screenshot 2025-11-30 at 10.25.31 PM" style="zoom:67%;" />

### Choosing among unbiased estimators-Example

* We see empirically that $\widetilde{\theta}$ is much less variable than $\widehat{\theta}$
* But also theoretically, $Var[\widetilde{\theta}]=\frac{\theta^{2}}{n(n+2)}$ and $Var[\widehat{\theta}]=\frac{\theta^{2}}{3n}$
* So, $Var[\widetilde{\theta}] < Var[\widehat{\theta}]$, for $n \ge 2$ and goes much faster to zero!
* Additionally, $\widehat{\theta}$ can take values way over the true $\theta$
* So, $\widetilde{\theta}$ is a much better estimate of $\theta$ than $\widehat{\theta}$

### Mean square error

* Although **unbiasedness** is a desirable property, unbiased estimators do not always exist
* Even when they exist, requiring unbiasedness maybe too stringent (i.e. there can be other good estimators that are biased)
* A general performance of an estimator can be judged by the way it spreads around the parameter to be estimated:
  - If $T$ is an estimator for a parameter $\theta$, the **mean squared error** of $T$ is the number:
    $$MSE(T) = E[(T-\theta)^2]$$

* It's easy to show that $MSE(T) = Var(T) + Bias(T)^2$ where $Bias(T) = E[T]-\theta$
* A **biased estimator** with a small bias could be more useful than an **unbiased estimator** with a large variance.
* Better to use $MSE(T)$ to choose between estimators
* When $Bias(T)=0$, $MSE(T) = Var(T)$

### Mean square error - example

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} Poisson(\mu)$

Two candidate estimators for $p_{0}=P(X_{i}=0)=e^{-\mu}$:

* $\widetilde{p}_{0}=\frac{\text{number of } X_{i}=0}{n}$
* $\widehat{p}_{0}=e^{-\overline{X_{n}}}$

$\widetilde{p}_{0}$ is unbiased but $\widehat{p}_{0}$ is not? Which one is better?

### Mean square error - example

Simulation to see how the two estimators behave

* True $p_{0}=e^{-2} \approx 0.135$

<img src="Lecture 9.assets/Screenshot 2025-11-30 at 10.47.20 PM.png" alt="Screenshot 2025-11-30 at 10.47.20 PM" style="zoom:50%;" />

### Mean square error - example

<img src="Lecture 9.assets/Screenshot 2025-11-30 at 10.47.59 PM.png" alt="Screenshot 2025-11-30 at 10.47.59 PM" style="zoom:50%;" />

