1. Consider the following inverse of the model matrix:

$$(X'X)^{-1} =
\begin{bmatrix}
0.893758 & -0.028245 & -0.0175641 \\
-0.028245 & 0.0013329 & 0.0001547 \\
-0.017564 & 0.0001547 & 0.0009108
\end{bmatrix}$$

(a) How many variables are in the regression model?  

(b) If the estimate of $$\sigma^2$$ is 50, what is the estimate of the variance of each regression coefficient?  

(c) What is the standard error of the intercept?



###### In Class Answer

$$
\hat\beta = (X'X)^{-1}X'Y
\\
$$



k+1 = p, p is the size of your model, $p \times p$ matrix

$Cov(\hat\beta) = \sigma^2 * C_{jj}$

$C = (X'X)^{-1}, j = 0, 1, 2, ..$

So $Cov(\hat\beta_0) = \sigma^2C_{00} = 50*0.89$

$Var(\hat \beta _1) = \sigma^2C_{11} = 50*0.0013329$



#### Gemini Answer

##### (a) How many variables are in the regression model?

There are **2 independent (predictor) variables** in this model.

**Here is why:** The given $(X'X)^{-1}$ matrix is a 3 by 3 matrix, which means the regression model estimates a total of 3 parameters (typically $\beta_0, \beta_1, \text{and } \beta_2$). Since one of these parameters accounts for the intercept ($\beta_0$), the remaining 2 parameters correspond to the independent variables.

##### (b) Estimate of the variance of each regression coefficient

The variance-covariance matrix of the estimated regression coefficients, $\hat{\beta}$, is given by the formula:

$$\text{Var}(\hat{\beta}) = \hat{\sigma}^2(X'X)^{-1}$$

The estimated variance for each individual coefficient lies on the main diagonal of this matrix. To find them, we simply multiply the diagonal elements of your $(X'X)^{-1}$ matrix by the estimated error variance ($\hat{\sigma}^2$), which is 50.

- **Variance of the intercept** ($\hat{\beta}_0$): $50 \times 0.893758 = \mathbf{44.6879}$
- **Variance of the first variable's coefficient** ($\hat{\beta}_1$): $50 \times 0.0013329 = \mathbf{0.066645}$
- **Variance of the second variable's coefficient** ($\hat{\beta}_2$): $50 \times 0.0009108 = \mathbf{0.04554}$

##### (c) Standard error of the intercept

The standard error of any regression coefficient is simply the square root of its estimated variance.

Taking the variance of the intercept we calculated in part (b):

$$\text{SE}(\hat{\beta}_0) = \sqrt{44.6879} \approx \mathbf{6.6849}$$



---



2. You have fit a regression model with two regressors to a data set that has 20 observations. The total sum of squares is 1000 and the model sum of squares is 750.  

(a) What is the value of $$R^2$$ for this model?  

(b) What is the adjusted $$R^2$$ for this model?  

(c) What is the value of the $$F$$-statistic for testing the significance of regression? What conclusions would you draw about this model if $$\alpha = 0.05$$? What if $$\alpha = 0.01$$? 

(d) Suppose you add a third regressor to the model and as a result, the model sum of squares is now 785. Does it seem that adding this factor has improved the model?



###### In-class review

Given n = 20, SST = 1000, SSR = 750, k = 2, p = 3

(a)
$$
R^2 = \frac{SSR}{SST} = \frac{750}{1000} = 0.75
$$
(b)
$$
R_{adj}^2 = \frac{SSR/k}{SST/n-1} = \frac{750/2}{1000/19} = 0.72
$$
(c)
$$
F_0 = \frac{MS_R}{MS_E} = \frac{SSR/k}{SSE/(n-p)} = \frac{750/2}{250/(20-3)} = 25.5
$$

$$
\alpha = 0.05
\\
f_{\alpha, v_1, v_2} = f_{0.05, 2, 17} = 3.59
$$

Because $v_1 = k = 2$,  $v_2 = n-p = 19-2 = 17$

Since $25.5 > 3.59$, we reject H0: $\beta_1 = \beta_2 = 0$

H1: at least one of them is not 0, $\beta_j \ne 0$
$$
\alpha = 0.01
\\
f_{\alpha, v_1, v_2} = f_{0.0, 2, 17} = 6.11
$$
25.5 still bigger than 6.11, still significant

(d)

New given
$$
SSR' = 785, k' = 3, p' = 4
$$

$$
F_0 = \frac{\Delta SSR}{MSE(full)} = \frac{SSR_{full}-SSR_{sub}}{MSE_{full}}
$$

Full model  $y = \beta_0 + \beta_1x_1+\beta_2x_2 + \beta_3x_3$

Submodel $y = \beta_0 + \beta_1x_1+\beta_2x_2$

But in this question, SSR is given so we just
$$
F_0 = \frac{\Delta SSR/R}{MSE(full)} = \frac{SSR_{full}-SSR_{sub}/1}{MSE_{full}} = \frac{780-750}{
\frac{SSE_{full}}{n-p'} = \frac{1000-785}{20-4} = 215/16
} = 2.6
$$

$$
SST = \sum_{i=1}^n (y_i - \bar y)^2 = 1000
$$

$$
f_{0.05, 1, 16} = 4.49
$$

Conclusion: compare 2.6 with critical value 4.49, cannot reject H0 hypothesis, the new $\beta_3$, theoretically is equal to 0.



#### Gemini Answer

##### (a) Value of $R^2$

The coefficient of determination, $R^2$, represents the proportion of the total variance explained by the model. It is calculated as the Model Sum of Squares ($SSM$) divided by the Total Sum of Squares ($SST$).

$$R^2 = \frac{SSM}{SST} = \frac{750}{1000} = \mathbf{0.75}$$

This means 75% of the variability in your dependent variable is explained by these two regressors.

##### (b) Adjusted $R^2$

The adjusted $R^2$ penalizes the model for adding extra predictors, making it a more reliable metric when comparing models with different numbers of variables.

Given $n = 20$ observations and $k = 2$ regressors, the formula is:

$$R^2_{adj} = 1 - (1 - R^2) \left( \frac{n - 1}{n - k - 1} \right)$$

$$R^2_{adj} = 1 - (1 - 0.75) \left( \frac{20 - 1}{20 - 2 - 1} \right)$$

$$R^2_{adj} = 1 - 0.25 \left( \frac{19}{17} \right) \approx \mathbf{0.7206}$$

##### (c) $F$-statistic and Significance

The $F$-statistic tests the overall significance of the regression model. To calculate it, we first need the Sum of Squares for Error ($SSE$), which is $SST - SSM = 1000 - 750 = 250$.

The formula for the $F$-statistic is the Mean Square Model ($MSM$) divided by the Mean Square Error ($MSE$):

$$F = \frac{SSM / k}{SSE / (n - k - 1)}$$

$$F = \frac{750 / 2}{250 / 17} = \frac{375}{14.7059} \approx \mathbf{25.5}$$

To draw conclusions, we compare our calculated $F$-statistic (25.5) to the critical value from the $F$-distribution with $df_1 = 2$ and $df_2 = 17$:

- **If $\alpha = 0.05$:** The critical $F$-value is approximately 3.59. Since 25.5 > 3.59, we reject the null hypothesis. The model is statistically significant.
- **If $\alpha = 0.01$:** The critical $F$-value is approximately 6.11. Since 25.5 > 6.11, we still reject the null hypothesis. The model is highly significant even at this stricter threshold.

##### (d) Evaluating the Third Regressor

##### 1. State the Hypotheses

Let the third regressor be associated with the coefficient $\beta_3$.

- **Null Hypothesis ($H_0$):** $\beta_3 = 0$ (Adding the third variable does *not* significantly improve the model).
- **Alternative Hypothesis ($H_a$):** $\beta_3 \neq 0$ (Adding the third variable *does* significantly improve the model).

##### 2. The Partial $F$-test Formula

The formula compares the "Full Model" (3 regressors) to the "Reduced Model" (2 regressors).
$$
F = \frac{(SSM_{full} - SSM_{reduced}) / p}{SSE_{full} / (n - k_{full} - 1)}
$$
Where:

- **$SSM_{full}$** = Model Sum of Squares for the new model = $785$
- **$SSM_{reduced}$** = Model Sum of Squares for the old model = $750$
- **$p$** = Number of additional regressors = $3 - 2 = 1$
- **$SSE_{full}$** = Sum of Squares Error for the full model = Total Sum of Squares ($SST$) - $SSM_{full}$ = $1000 - 785 = 215$
- **$n$** = Total number of observations = $20$
- **$k_{full}$** = Total regressors in the new model = $3$

##### 3. Step-by-Step Calculation

First, calculate the numerator (the "extra" variance explained by the new variable):

$$\text{Numerator} = \frac{785 - 750}{1} = \frac{35}{1} = \mathbf{35}$$

Next, calculate the denominator (the Mean Square Error of the full model):

$$\text{Denominator} = \frac{215}{20 - 3 - 1} = \frac{215}{16} = \mathbf{13.4375}$$

Finally, divide the two to get your partial $F$-statistic:

$$F = \frac{35}{13.4375} \approx \mathbf{2.605}$$

##### 4. Determine Significance and Conclude

To find out if this is significant at $\alpha = 0.05$, we compare our calculated $F$-statistic (2.605) to the critical value from an $F$-distribution table with:

- $df_1$ (numerator degrees of freedom) = $p = 1$
- $df_2$ (denominator degrees of freedom) = $n - k_{full} - 1 = 16$

The critical $F$-value for $F(1, 16)$ at $\alpha = 0.05$ is **4.494**.

**Conclusion:** Because our calculated $F$-statistic (2.605) is *less than* the critical value (4.494), we **fail to reject the null hypothesis**. At the 5% significance level, the addition of the third regressor is **not statistically significant**.

---



3. Answer the following questions:

(a) If the Bayes decision boundary is linear, do we expect LDA or QDA to perform better on the training set? On the test set?  

(b) If the Bayes decision boundary is non-linear, do we expect LDA or QDA to perform better on the training set? On the test set?  

(c) In general, as the sample size $$n$$ increases, do we expect the test prediction accuracy of QDA relative to LDA to improve, decline, or be unchanged? Why?  

(d) True or False: Even if the Bayes decision boundary for a given problem is linear, we will probably achieve a superior test error rate using QDA rather than LDA because QDA is flexible enough to model a linear decision boundary. Justify your answer.



###### In Class Review

(a)

QDA is nonlinear, more flexible, more complex, fits your data better. On the test data set, LDA would do better, the reason is underlying true model is linear, so underlying is better

(b)

QDA would perform better on both dataset.

(c)

QDA perform better for training dataset, the prediction accuracy of QDA would improve, n increase to some extent the flexible model doing better for prediction

(d)

False, even though QDA can fit your dataset better. But it is overfitting, performance for prediction is worse and the variance for flexible model is higher.



#### Gemini Answer

##### (a) When the Bayes decision boundary is linear

- **Training Set:** We expect **QDA** to perform better. QDA is a more flexible model because it estimates a separate covariance matrix for each class, giving it more parameters to tweak. Because of this flexibility, it can fit the training data more closely than LDA, yielding a lower training error rate.
- **Test Set:** We expect **LDA** to perform better. Since the true decision boundary is linear, LDA's core assumption (that classes share a common covariance matrix) perfectly matches reality. QDA, being more flexible, will likely overfit the noise in the training data, leading to higher variance and a higher error rate on the unseen test set.

(b) When the Bayes decision boundary is non-linear

- **Training Set:** We expect **QDA** to perform better. Its quadratic nature allows it to easily mold to the non-linear patterns in the training data, whereas LDA is rigidly constrained to straight lines (or flat planes).
- **Test Set:** We expect **QDA** to perform better. LDA will suffer from high bias because its linear assumption completely misses the true non-linear nature of the data. QDA's flexibility allows it to approximate the true non-linear Bayes decision boundary much more accurately, reducing bias and improving test performance.

##### (c) As sample size $n$ increases

We expect the test prediction accuracy of QDA relative to LDA to **improve**.

**Why:** This comes down to the bias-variance tradeoff. QDA is a highly flexible model that requires estimating significantly more parameters than LDA. When the sample size $n$ is small, QDA's flexibility causes high variance, leading to overfitting. However, as $n$ becomes very large, the variance introduced by estimating those extra parameters diminishes. With enough data, QDA can accurately estimate the distinct covariance matrices without overfitting, allowing its lower bias (its ability to model more complex shapes) to shine.

##### (d) True or False

**False.** **Justification:** If the true Bayes decision boundary is linear, LDA is the ideal model because its assumptions exactly match the data generation process. While it is true that QDA *can* model a linear boundary, doing so comes at a cost. QDA achieves its flexibility by estimating a separate covariance matrix for every single class, which consumes a large number of parameters. This extra flexibility introduces unnecessary variance into the model. Instead of just fitting the linear boundary, QDA will try to fit the random noise in the training data (overfitting). Therefore, QDA will generally yield a *worse* (inferior) test error rate than LDA when the true boundary is linear.

---



4. There is a set of data ($$n = 100$$ observations) containing a single predictor and a quantitative response. Then fit a linear regression model to the data, as well as a separate cubic regression, i.e.,  

$$Y = \beta_0 + \beta_1 X + \beta_2 X^2 + \beta_3 X^3 + \varepsilon.$$

(a) Suppose that the true relationship between $$X$$ and $$Y$$ is linear, i.e.,  

$$Y = \beta_0 + \beta_1 X + \varepsilon.$$

Consider the training residual sum of squares (RSS) for the linear regression, and also the training RSS for the cubic regression. Would we expect one to be lower than the other, would we expect them to be the same, or is there not enough information to tell? Justify your answer. How about using test rather than training RSS?  

(b) Suppose that the true relationship between $$X$$ and $$Y$$ is not linear, but we don’t know how far it is from linear. Consider the training RSS for the linear regression, and also the training RSS for the cubic regression. Would one be lower than the other, would we expect them to be the same, or is there not enough information to tell? Justify your answer. How about using test rather than training RSS?



###### In class review

(a)

cubic regression model will fit better for training RSS, but simple linear regression will give you better prediction in test RSS

(b)

Cubic model would fit better for training since it is more flexible. But since we don't actually know the true relationship for this (how far it is from linear), so we don't have enough info which model doing better in prediction. 



#### Gemini Answer

##### (a) When the true relationship is linear

- **Training RSS:** We expect the **cubic regression** to have a lower (or at least equal) training RSS.
  - **Justification:** The cubic model is more flexible because it has more parameters (degrees of freedom). Mathematically, it encompasses the linear model (if it estimates $\beta_2 = 0$ and $\beta_3 = 0$). Because of this added flexibility, the cubic model will essentially try to chase and fit the random, irreducible error ($\varepsilon$) in the training data. This overfitting inherently drives the training RSS down compared to the stricter linear model.
- **Test RSS:** We expect the **linear regression** to have a lower test RSS.
  - **Justification:** Since the true underlying relationship is linear, the linear model captures the actual signal without overfitting the noise. The cubic model, having overfit the specific noise of the training set, will generalize poorly to new, unseen data. This excess variance in the cubic model leads to a higher test RSS.

##### (b) When the true relationship is non-linear (but form is unknown)

- **Training RSS:** We expect the **cubic regression** to have a lower training RSS.
  - **Justification:** The reasoning remains exactly the same as in part (a). Regardless of the true underlying shape, a more flexible model (cubic) will always be able to fit the training data points more closely than a less flexible model (linear), thereby minimizing the training RSS.
- **Test RSS:** There is **not enough information to tell**.
  - **Justification:** This outcome depends entirely on *how* non-linear the true relationship actually is, which brings us to the bias-variance tradeoff:
    - If the true relationship is only very slightly non-linear (i.e., close to linear), the linear model might still perform better on the test set because the cubic model's high variance could outweigh its slight reduction in bias.
    - If the true relationship is highly non-linear (e.g., truly cubic or quadratic), the linear model will suffer from very high bias (underfitting). In this scenario, the cubic model's ability to capture the non-linear shape will likely overcome its variance penalty, resulting in a lower test RSS.

---

5.

Suppose we collect data for a group of students in a statistics class with variables $$X_1 =$$ hours studied, $$X_2 =$$ undergrad GPA, and $$Y =$$ receive an A. We fit a logistic regression and produce estimated coefficients,  

$$\hat{\beta}_0 = -6, \quad \hat{\beta}_1 = 0.05, \quad \hat{\beta}_2 = 1.$$

(a) Estimate the probability that a student who studies for 40 hours and has an undergrad GPA of 3.5 gets an A in the class.  

(b) How many hours would the student in part (a) need to study to have a $$50\%$$ chance of getting an A in the class?



###### In class review

y = 1 for successful get A, 0 for not getting A
$$
P(y = 1| x) = \frac{e^{\beta0+\beta1x1+\beta2x2}}{1+e^{\beta0+\beta1x1+\beta2x2}}
$$

$$
P(y = 0| x) = \frac{1}{1+e^{\beta0+\beta1x1+\beta2x2}}
$$

$$
\beta_0 = -6, \beta_1 = 0.05, \beta_2=1
$$

(a)

$(-6)+(0.05)(40)+(1)(3.5) = -0.5$
$$
\frac{e^{-0.5}}{1+e^{-0.5}} = 0.3775
$$


(b)

$$\log\left(\frac{p}{1-p}\right) = \hat{\beta}_0 + \hat{\beta}_1 X_1 + \hat{\beta}_2 X_2$$

since $p=0.5$, $log(0.5/0.5 = 1) = log(1) = 0$

so $(-6) + (0.05)X_1 + 1(3.5) = 0$, $X1 = 50$



##### Gemini Answer

##### (a) Estimating the probability of getting an A

Logistic regression models the log-odds of an event occurring as a linear combination of the predictors:

$$\log\left(\frac{p}{1-p}\right) = \hat{\beta}_0 + \hat{\beta}_1 X_1 + \hat{\beta}_2 X_2$$

To find the probability $p$, we rearrange the formula to solve for $p$:
$$
p = \frac{e^{\hat{\beta}_0 + \hat{\beta}_1 X_1 + \hat{\beta}_2 X_2}}{1 + e^{\hat{\beta}_0 + \hat{\beta}_1 X_1 + \hat{\beta}_2 X_2}}
$$
First, calculate the value of the linear equation using the given coefficients and the student's information ($X_1 = 40$ hours, $X_2 = 3.5$ GPA):

$$\text{Log-odds} = -6 + 0.05(40) + 1(3.5)$$

$$\text{Log-odds} = -6 + 2 + 3.5 = -0.5$$

Next, plug this result into the probability equation:
$$
p = \frac{e^{-0.5}}{1 + e^{-0.5}}
$$

$$
p \approx \frac{0.6065}{1 + 0.6065} \approx \frac{0.6065}{1.6065} \approx \mathbf{0.3775}
$$

The estimated probability that this student gets an A is approximately **37.75%**.

##### (b) Hours needed for a 50% chance

To find the hours required for a **50%** chance ($p = 0.5$), we need the log-odds to equal 0.

**Here is why:** $\log\left(\frac{0.5}{1 - 0.5}\right) = \log(1) = 0$.

Set the linear part of the model to 0, plug in the student's GPA ($X_2 = 3.5$), and solve for hours studied ($X_1$):

$$-6 + 0.05(X_1) + 1(3.5) = 0$$

$$-6 + 0.05 X_1 + 3.5 = 0$$

$$-2.5 + 0.05 X_1 = 0$$

$$0.05 X_1 = 2.5$$

$$X_1 = \frac{2.5}{0.05} = \mathbf{50}$$

The student would need to study for **50 hours** to reach a **50%** probability of getting an A in the class.

---

6. Suppose that we wish to predict whether a given stock will issue a dividend this year (“Yes” or “No”) based on $$X$$, last year’s percent profit. We examine many companies and discover that the mean value of $$X$$ for companies that issued a dividend was $$\bar{X} = 10$$, while the mean for those that did not was $$\bar{X} = 0$$. In addition, the variance of $$X$$ for these two sets of companies was $$\hat{\sigma}^2 = 36$$. Finally, $$80\%$$ of companies issued dividends. If $$X$$ follows a normal distribution, predict the probability that a company will issue a dividend this year given that its percentage profit was $$X = 4$$ last year.



###### In class review

Y

| Yes = 1 | 0.8  | $\bar X = 10$ | $\hat\sigma^2 = 36$ |      |
| ------- | ---- | ------------- | ------------------- | ---- |
| No = 0  | 0.2  | $\bar X = 0$  | $\hat\sigma^2 = 36$ |      |

X = 4


$$
P(Y=1|X) = \frac{\pi_kP(X|Y)}{P(X)}
\\
P(Y=1|X) = \frac{\pi_kf_k(x)}{\sum^2_{l=1}\pi_lf_l(x)}
\\
= \frac{
0.8\frac{1}{\sqrt{2\pi}\sigma^2}e^{-\frac{(4-10)^2}{2*36}}
}{0.8\frac{1}{\sqrt{2\pi}\sigma^2}e^{-\frac{(4-10)^2}{2*36}} + 0.2\frac{1}{\sqrt{2\pi}\sigma^2}e^{-\frac{(4-0)^2}{2*36}}}
\\
=\frac{0.8 e^{1/2}}{0.8e^{1/2}+0.2e^{-2/9}}
\\
=0.75
$$

$$
f_k(x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{1}{2\sigma^2}(x - \mu_k)^2\right)
$$



#### Gemini Answer

##### 1. Identify the Given Parameters

First, let's lay out the information provided for our two classes, "Yes" (issued a dividend) and "No" (did not issue):

- **Priors ($\pi$):** The overall probability of each class.
  - $\pi_{\text{Yes}} = 0.80$ (80% of companies issued dividends)
  - $\pi_{\text{No}} = 0.20$ (The remaining 20% did not)
- **Means ($\mu$):** 
  - $\mu_{\text{Yes}} = 10$
  - $\mu_{\text{No}} = 0$
- **Variance ($\sigma^2$):** $\sigma^2 = 36$ (shared between both classes)
- **Observed Value ($x$):** $x = 4$

##### 2. The Formula

According to Bayes' theorem, the probability that a company belongs to class $k$ given observation $x$ is:
$$
P(Y = k \mid X = x) = \frac{\pi_k f_k(x)}{\sum_{l=1}^{K} \pi_l f_l(x)}
$$
Where $f_k(x)$ is the normal density function for class $k$:

$$f_k(x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{1}{2\sigma^2}(x - \mu_k)^2\right)$$

*Note: Because the variance ($\sigma^2$) is the same for both classes, the constant term $\frac{1}{\sqrt{2\pi\sigma^2}}$ will appear in every part of the numerator and denominator, meaning it cancels out entirely. We only need to calculate the exponential part!*

##### 3. Calculate the Exponential Densities

Let's plug $x = 4$ into the exponential part of the density function for both classes.

**For "Yes" (Issued Dividend):**

$$E_{\text{Yes}} = \exp\left(-\frac{1}{2(36)}(4 - 10)^2\right)$$

$$E_{\text{Yes}} = \exp\left(-\frac{1}{72}(-6)^2\right)$$

$$E_{\text{Yes}} = \exp\left(-\frac{36}{72}\right) = \exp(-0.5) \approx \mathbf{0.6065}$$

**For "No" (Did Not Issue):**

$$E_{\text{No}} = \exp\left(-\frac{1}{2(36)}(4 - 0)^2\right)$$

$$E_{\text{No}} = \exp\left(-\frac{1}{72}(16)\right)$$

$$E_{\text{No}} = \exp\left(-\frac{16}{72}\right) \approx \exp(-0.2222) \approx \mathbf{0.8007}$$

##### 4. Calculate the Final Probability

Now we plug our priors and calculated densities back into Bayes' Theorem to find the probability of "Yes" given $X = 4$:
$$
P(Y = \text{Yes} \mid X = 4) = \frac{\pi_{\text{Yes}} E_{\text{Yes}}}{\pi_{\text{Yes}} E_{\text{Yes}} + \pi_{\text{No}} E_{\text{No}}}
\\
P(Y = \text{Yes} \mid X = 4) = \frac{0.80(0.6065)}{0.80(0.6065) + 0.20(0.8007)}
\\
P(Y = \text{Yes} \mid X = 4) = \frac{0.4852}{0.4852 + 0.1601}
\\
P(Y = \text{Yes} \mid X = 4) = \frac{0.4852}{0.6453} \approx \mathbf{0.7519}
$$
There is approximately a **75.19%** probability that the company will issue a dividend this year.



---

7. Usually, for two classes coded as $$(0, 1)$$, the probability from a logistic model can be written as  

$$
\Pr(y = 1 \mid X) = \frac{e^{X'\beta}}{1 + e^{X'\beta}}
\quad \text{and} \quad
\Pr(y = 0 \mid X) = \frac{1}{1 + e^{X'\beta}}
$$

However, if two classes are coded as $$(-1, 1)$$, the probability can be written as  

$$
\Pr(y = 1 \text{ or } -1 \mid X) = \frac{1}{1 + e^{-y X'\beta}}
$$

Explain why? Write out the Bernoulli PMF function for $$y = (-1 \text{ or } 1)$$.



###### In class review

When you plug in y = 1
$$
P(y = 1 \mid X) = \frac{1}{1 + e^{-X'\beta}}
\\
P(y=-1|X) = \frac{1}{1+e^{X'\beta}}
$$
For the first equation, if times

$e^{X'\beta}$

for both sides, they are essentially same equation



for bernouli PMF, y = 1 success, = 0 failure

$P(y) = P^y(1-P)^{1-y}$

$P(y=1) = p$, $P(y=0) = 1-p$



but if y = 1success, = -1 failure
$$
P(y) = P^{(y+1)/2}(1-p)^{1-\frac{y+1}{2}}
$$
we need to make sure when y = -1, first exponent =0, and second exponent = 1



##### Gemini Answer

##### Why the $\{-1, 1\}$ Formulation Works

The standard $(0, 1)$ formulation uses two separate equations depending on the class. However, by rewriting the equation for $\Pr(y = 1 \mid X)$ slightly, we can see how the $\{-1, 1\}$ formulation unifies them into a single, symmetric equation.

First, let's rewrite the standard probability for the positive class by dividing the numerator and denominator by $e^{X'\beta}$:
$$
\Pr(y = 1 \mid X) = \frac{e^{X'\beta}}{1 + e^{X'\beta}} = \frac{1}{e^{-X'\beta} + 1} = \frac{1}{1 + e^{-X'\beta}}
$$
Now, let's test the proposed unified equation, $\Pr(y \mid X) = \frac{1}{1 + e^{-y X'\beta}}$, for both possible values of $y$:

- **Case 1: When $y = 1$ (Positive Class)**

  Substitute $1$ for $y$ in the exponent:

  $$\Pr(y = 1 \mid X) = \frac{1}{1 + e^{-(1) X'\beta}} = \frac{1}{1 + e^{-X'\beta}}$$

  This perfectly matches our rewritten standard probability for the positive class.

- **Case 2: When $y = -1$ (Negative Class)**

  Substitute $-1$ for $y$ in the exponent:
  $$
  \Pr(y = -1 \mid X) = \frac{1}{1 + e^{-(-1) X'\beta}} = \frac{1}{1 + e^{X'\beta}}
  $$
  This perfectly matches the standard probability for the negative class (which was previously coded as $0$).

**Conclusion:** By coding the classes as $\{-1, 1\}$, the value of $y$ itself acts as a mathematical switch. It flips the sign of the exponent $X'\beta$, allowing a single logistic function to compute the correct probability for whichever class is observed. This makes mathematical proofs and gradient calculations in machine learning much cleaner.

------

##### The Bernoulli PMF for $y \in \{-1, 1\}$

The standard Bernoulli PMF for a variable $Y \in \{0, 1\}$ with probability of success $p$ is written as:

$$\Pr(Y = y) = p^y (1 - p)^{1 - y}$$

To adapt this for $Y \in \{-1, 1\}$, we need an exponent that equals $1$ when $y=1$ and $0$ when $y=-1$ (to isolate $p$), and vice-versa (to isolate $1-p$). We can achieve this using the linear transformation $\frac{1 + y}{2}$.

Let $p = \Pr(Y = 1)$. The modified Bernoulli PMF is:
$$
\Pr(Y = y) = p^{\frac{1 + y}{2}} (1 - p)^{\frac{1 - y}{2}}
$$
**Let's verify it:**

- If $y = 1$: The exponent of $p$ becomes $\frac{1 + 1}{2} = 1$, and the exponent of $(1-p)$ becomes $\frac{1 - 1}{2} = 0$. The result is $p$.
- If $y = -1$: The exponent of $p$ becomes $\frac{1 - 1}{2} = 0$, and the exponent of $(1-p)$ becomes $\frac{1 - (-1)}{2} = 1$. The result is $1 - p$.

Alternatively, if you are looking for the conditional PMF directly in terms of the logistic regression parameters $\beta$ and input $X$, it is simply the unified equation we proved in the first section:
$$
\Pr(Y = y \mid X) = \frac{1}{1 + e^{-y X'\beta}}
$$
