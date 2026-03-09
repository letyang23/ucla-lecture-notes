# 1/12 Lecture 1

### **Course Logistics & Overview**

* **Course:** ISE 529: Predictive Analytics.


* **Instructor:** Prof. Tao Ma.


  * **Office:** GER 216.


  * **Office Hours:** Wednesday, 2:30 PM – 3:30 PM.


  * **Communication:** Appointments available by email if office hours don't fit; open to in-person meetings .


* **Teaching Assistant:** Rhea Huang.


  * **Office Hours:** Monday, 2:00 PM – 4:00 PM (same building) .


  * **Role:** Contact for homework questions and grading issues.


* **Format:** Two sections (regular in-person and online) managed via **Brightspace**.


* **Prerequisites:** Fundamental knowledge of Python programming, statistical probability models, and linear algebra.

---

### **Grading Structure**

* **Homework (25%):**

  * 5 required assignments + 1 optional bonus assignment (Homework 6) .


  * **Late Policy:**


    * 1 day late: 20% deduction.


    * 2 days late: 50% deduction.


    * more than 2 days late: Not accepted (0 grade).


  * **Submission:** Submit via Brightspace only; do not email homework.


* **Midterm Exam (30%):** In-person.


* **Final Exam (40%):** In-person, non-cumulative (no overlap with midterm).


* **Bonus Points (Up to 3 pts):** Based on attendance and participation. These are added to the final grade and can lift a letter grade (e.g., from A- to A) .

**Exam Rules:**

* Exams are **Open Book** (hard copies allowed, cheat sheets allowed) .


* **No Electronics:** No internet access, laptops, or phones allowed during the exam .


* **Attendance:** Mandatory for exams; no make-up exams allowed .

---

### **Course Content: Key Takeaways**

The course covers four major modules focused on theory (lectures) and application (homework).

**1. Quantitative/Numerical Predictions**

* Focuses on regression techniques.


* **Models:** Simple/Multiple linear regression, Polynomial regression, Ridge & Lasso, Principal Component Regression (PCR), Partial Least Squares (PLS).

**2. Classification**

* Predicting the probability that an input belongs to a specific class (e.g., Yes vs. No, image recognition) .


* **Models:** Logistic Regression, Linear Discriminant Analysis (LDA), Quadratic Discriminant Analysis (QDA), Naive Bayes, Support Vector Machines (SVM) .

**3. Tree-Based Methods**

* Used for both numerical prediction and classification .


* **Techniques:** Decision Trees, Bagging, Random Forest, Boosting .

**4. Deep Learning (Neural Networks)**

* Includes theory and practical implementation.


* **Multi-layer Perceptrons (MLP):** For numerical data .


* **Convolutional Neural Networks (CNN):** For image data/pattern recognition .


* **Recurrent Neural Networks (RNN):** For time-series data.

---

### **Software & Technical Setup**

**1. Python Requirements**

* **Version:** You **MUST** install **Python 3.10** (specifically 3.10.9 recommended).

  * *Reason:* Newer versions (3.11+) are not yet compatible with **TensorFlow** .


* **Required Libraries:** Numpy, Pandas, Scikit-learn (sklearn), Statsmodels, TensorFlow.

**2. IDE Options (Integrated Development Environments)**

* **JupyterLab (Recommended):** The standard environment for the course. Files saved as `.ipynb`.


* **PyCharm (Advanced):** Recommended for students with Computer Science backgrounds or advanced users. Files saved as `.py`.


* **Google Colab (Alternative):** A cloud-based "dummy environment" that requires no installation. Useful if you struggle with local setup.

**3. Hardware Requirements**

* **Standard Homework:** A personal laptop (CPU/GPU) is sufficient for Homework 1-5.


* **Bonus Homework (HW6):** Requires High-Performance Computing (HPC).


  * Involves a large dataset (20,000+ images) that may crash personal laptops.


  * Students will be given access to the USC HPC cluster (Linux-based) .


  * *Alternative:* Viterbi Virtual Desktop (available but limited to 8-hour run times) .

---

### **Installation Guide (Step-by-Step)**

**Installing Python (Windows/Mac)**

1. **Download:** Go to the official Python website and download **Python 3.10**.


2. **Windows Setup:** When installing, **check the box "Add Python to PATH"** (crucial for the OS to find the software) .


3. **Linux Setup:** Update the `.bashrc` file to include the path to the software .

**Installing Libraries (pip)**

1. Open your Terminal (Mac/Linux) or Command Prompt (Windows) .


2. Use the `pip` command (Python's packaging tool) to install libraries from the PyPI repository.


* *Command:* `pip install [library_name]` (e.g., `pip install tensorflow`).

**Optional: Miniconda**

* Can be used to manage environments and multiple Python versions.


* Allows creation of virtual environments so you don't mess up your base operating system.

**Running Code**

* **JupyterLab:** Start by typing `jupyter lab` in the terminal from your project folder . It runs code in cells (interactive mode).


* **PyCharm:** Runs `.py` scripts. You can right-click a file and select "Run" .


* *Note:* You can run `.py` files inside JupyterLab using the command `%run filename.py` .

### **Next Steps for Students**

* Install Python 3.10 and set up the environment (JupyterLab/PyCharm) immediately.


* Respect the schedule: Exams are on March 4th and April 29th (dates may shift slightly, but these are targets) .


* Attendance is not tracked daily but is noticed for bonus points .





# 1/14 Lecture 2

### **I. Administrative & Course Logistics**

- **Lecture Context:** This session bridges the initial setup (from the previous lecture) to actual modeling techniques.
- **Resources:** The Python code examples and datasets (e.g., `auto.csv`, `Boston` data) demonstrated in class are available on **Brightspace** under the "Example" folder.
- **Recording:** Lecture recordings should be available on Brightspace, though technical issues were noted with the link visibility for some students.

------

### **II. Python Programming & Environment (Practical Demo)**

The instructor demonstrated core Python tasks using **JupyterLab**, the expected IDE for the course.

#### **1. Library Management & Aliasing**

- **Importing:** Use `import` to load libraries.
- **Aliasing:** Use short aliases to save time when calling functions (e.g., `import numpy as np`, `import pandas as pd`, `import statsmodels.api as sm`).
- **Inspection:** Use the `dir(module_name)` command to list all available functions within a library.

#### **2. File Opertions (OS & I/O)**

- **OS Module:**
  - `os.getcwd()`: Get current working directory.
  - `os.chdir(path)`: Change current directory.
- **Reading/Writing Files:**
  - **Writing:** Use `open('filename', 'w')`. Always pair with `.close()` to prevent memory leaks.
  - **Reading:** Use `open('filename', 'r')` and `.read()` .

#### **3. Data Manipulation with Pandas**

- **Loading Data:** Use `pd.read_csv('filename.csv')` to load data into a DataFrame (essentially a matrix with column titles).
- **Basic Operations:**
  - **Access Column:** `dataframe['column_name']`.
  - **Calculations:** `dataframe['column_name'].sum()`.
  - **Summary Stats:** `dataframe.describe()` provides statistics (count, mean, std, etc.) for the data .
- **Plotting:**
  - `dataframe.plot.scatter(x='col1', y='col2')` creates a scatter plot.
  - `pd.plotting.scatter_matrix(dataframe)` creates a grid of plots comparing variables .

#### **4. Linear Regression with Statsmodels**

- **Library:** `statsmodels` is used for statistical modeling.
  - Use `import statsmodels.api as sm`

- **Model Structure:** The goal is to estimate coefficients ($\beta$) for a linear regression model formatted as: $y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + ... + \beta_p x_p$.
- **Procedure:**
  1. **Prepare Data:** Define input matrix $X$ (predictors) and output vector $Y$ (response). The instructor used `Boston` housing data for this example .
  2. **Estimate Model:** Use Ordinary Least Squares (OLS).
     - Code structure: `model = sm.OLS(Y, X).fit()` .
  3. **Review Results:** Call `model.summary()` to see coefficients ($\beta_0, \beta_1$), R-squared, P-values, and standard errors .

#### **5. Custom Functions**

- **Definition:** Use the `def` keyword.
  - Example: `def abline(slope, intercept):` was created to plot a regression line on top of a scatter plot since no direct function existed for that specific task .

------

### **III. Review of Probability Models**

The instructor reviewed three foundational discrete probability models.

#### **1. Bernoulli Distribution**

- **Definition:** A binary random variable representing a single trial with two outcomes: Success (1) or Failure (0).

- **Parameter:** $p$ (probability of success). Probability of failure is $1-p$.

- **Probability Mass Function (PMF):**

  $$P(X=x) = p^x (1-p)^{1-x} \quad \text{for } x \in \{0, 1\}$$

  - If $x=1$ (success), probability is $p$.
  - If $x=0$ (failure), probability is $1-p$ .

#### **2. Binomial Distribution (The "Godfather")**

- **Context:** Describes the number of successes ($X$) in $n$ independent Bernoulli trials .

- **Parameters:**

  - $n$: Total number of trials.
  - $p$: Probability of success per trial.

- **PMF Formula:**

  $$P(X=x) = \binom{n}{x} p^x (1-p)^{n-x}$$

  - **Combinations ($\binom{n}{x}$):** Represents the number of ways to choose $x$ successes out of $n$ trials. Calculated as $\frac{n!}{x!(n-x)!}$ .
  - **Probability Term:** $p^x (1-p)^{n-x}$ represents the joint probability of one specific combination of outcomes .

- **Moments:**

  - Expectation: $E[X] = np$.
  - Variance: $Var(X) = np(1-p)$.

- **Origin:** Derived from the **Binomial Theorem**, which expands $(a+b)^n$. If $a=p$ and $b=1-p$, the sum of probabilities equals 1.

#### **3. Poisson Distribution**

- **History:** Proposed by Simeon Poisson (1837) to solve computational difficulties with the Binomial model when $n$ is very large (calculating large factorials was impossible) .

- **Use Case:** Approximates the Binomial distribution when:

  - $n$ is large (number of trials/opportunities).
  - $p$ is small (probability of success).
  - Represents the number of arrivals/occurrences in a unit of time or space .

- **Parameter:** $\lambda$ (Lambda), where $\lambda = np$. Represents the average success/arrival rate .

- **Derivation (Binomial Limit):**

  The instructor showed that as $n \to \infty$ and $p \to 0$ (keeping $\lambda = np$ constant), the Binomial PMF transforms into the Poisson PMF:

  $$\lim_{n \to \infty} \binom{n}{x} \left(\frac{\lambda}{n}\right)^x \left(1-\frac{\lambda}{n}\right)^{n-x} = \frac{e^{-\lambda}\lambda^x}{x!}$$

  - Key mathematical limit used: $\lim_{n \to \infty} (1 - \frac{\lambda}{n})^n = e^{-\lambda}$ .

- **PMF Formula:**

  $$P(X=x) = \frac{e^{-\lambda} \lambda^x}{x!}$$

- **Moments:**

  - Expectation: $E[X] = \lambda$.
  - Variance: $Var(X) = \lambda$.

#### **4. Example Problem (Typos in a Book)**

- **Scenario:** 1 typo occurs every 3 pages on average.

- **Task:** Find the probability of having **at least one** error on a single page .

- **Setup:**

  - Rate ($\lambda$): If 1 error per 3 pages, then for 1 page, $\lambda = 1/3$ (Note: The transcript cuts off slightly, but implies the rate calculation based on unit size).

  - Calculation strategy: Use the complement rule.

    $$P(X \geq 1) = 1 - P(X=0)$$

  - Where $P(X=0) = \frac{e^{-\lambda}\lambda^0}{0!} = e^{-\lambda}$ .



# 1/21 Lecture 3

### **I. Review of Probability Models**

The lecture began by reviewing foundational probability distributions that are critical for predictive modeling.

#### **1. Binomial Distribution**

- **Origin:** Derived from the **Binomial Theorem** learned in high school, which expands $(a+b)^n$ .

- **Binomial Theorem Formula:**

  $$(a+b)^n = \sum_{x=0}^{n} \binom{n}{x} a^x b^{n-x}$$

  - Where $\binom{n}{x} = \frac{n!}{x!(n-x)!}$ is the combination of $n$ items taken $x$ at a time.

- **Connection to Probability:** By setting $a = p$ (success probability) and $b = 1-p$ (failure probability):

  - The sum becomes $(p + (1-p))^n = 1^n = 1$. This proves that the Binomial PMF sums to 1 across the sample space, qualifying it as a valid probability mass function .

- **Limitations:** When $n$ (number of trials) is very large (approaching infinity) and $p$ is very small, the Binomial formula becomes computationally impossible due to the factorial terms . This led to the development of the Poisson distribution.

#### **2. Poisson Distribution**

- **Derivation:** Created by Siméon Denis Poisson (1837) to approximate the Binomial distribution when $n \to \infty$ and $p \to 0$.

- **Parameter:** $\lambda$ (Lambda).

  - $\lambda$ represents the average number of arrivals or occurrences per unit of time/space.
  - In the derivation from Binomial, $\lambda = n \times p$.

- **Formula Validity:** The instructor proved this is a valid PMF by showing that the sum of probabilities equals 1, utilizing the **Maclaurin series** expansion of $e^\lambda$ .

  - $\sum_{x=0}^{\infty} \frac{\lambda^x}{x!} = e^\lambda$.
  - Therefore, $\sum P(X=x) = e^{-\lambda} \cdot e^{\lambda} = 1$.

- **Extended Formula (Time-Dependent):**

  - To calculate probabilities over a specific time window $t$:

    $$P(N(t) = n) = \frac{(\lambda t)^n e^{-\lambda t}}{n!}$$

  - Here, $\lambda t$ represents the average number of occurrences during time window $t$ .

#### **3. Normal Distribution (Gaussian)**

- **History:** Abraham de Moivre (1733) first approximated the Binomial distribution for the special case $p=0.5$. Laplace later generalized this (Central Limit Theorem concept), and Gauss applied it to astronomy .

- **De Moivre-Laplace Theorem:**

  - If $X$ is a Binomial random variable, it can be approximated by a continuous integral:

    $$P\left(a \le \frac{X - np}{\sqrt{np(1-p)}} \le b\right) \approx \frac{1}{\sqrt{2\pi}} \int_{a}^{b} e^{-z^2/2} dz$$

  - The term $\frac{X - np}{\sqrt{np(1-p)}}$ represents the **standardized** variable (Z-score), where $np$ is the mean ($\mu$) and $\sqrt{np(1-p)}$ is the standard deviation ($\sigma$) .

- **Standard Normal Distribution ($Z$):**

  - $\mu = 0$ and $\sigma = 1$.

  - To calculate probabilities for any Normal variable $X \sim N(\mu, \sigma^2)$, you must standardize it first:

    $$Z = \frac{X - \mu}{\sigma}$$ (X-mean / std deviation)

  - Then, use the **Standard Normal Table (Z-table)** to find probabilities .

------

### **II. Conditional Probability & Bayes' Theorem**

#### **1. Conditional Probability**

- **Definition:** The probability of event $A$ occurring given that event $B$ has occurred.

  $$P(A|B) = \frac{P(A \cap B)}{P(B)}$$

- **Intuition:** The sample space "shrinks" from the entire universe to just the outcome space of $B$. The probability is the ratio of the overlap ($A \cap B$) to the condition ($B$) .

- **Example (Course Prerequisites):**

  - 70% passed Calculus ($P(C)=0.7$).
  - 15% passed Discrete Math ($P(D)=0.15$).
  - 45% of Discrete Math students also passed Calculus (Joint $P(C \cap D)$ implied as overlap, though example numbers were slightly confusing in transcript, calculation was $0.45 / 0.7$) .

#### **2. Bayes' Theorem**

- **Formula:**

  $$P(A|B) = \frac{P(B|A)P(A)}{P(B)}$$

- **Why use it?** Often, calculating $P(A|B)$ directly is difficult, but the reverse conditional $P(B|A)$ is known or easy to obtain .

- **Total Probability Rule (Denominator):** $P(B)$ is often calculated by summing all disjoint scenarios:

  $$P(B) = \sum P(B|A_i)P(A_i)$$

- **Example (Defective Product):**

  - Machines 1, 2, 3 produce 15%, 30%, 55% of products respectively.

  - Defect rates: M1=4%, M2=5%, M3=3% .

  - *Question:* If a product is defective, what is the probability it came from Machine 3?

  - *Solution:*

    $$P(M3|Defect) = \frac{P(Defect|M3)P(M3)}{P(Defect)}$$

  - *Calculation:* Use weighted sum for the denominator (Total Defect Rate) .

------

### **III. Statistical Concepts: Expectation & Variance**

#### **1. Expectation ($E[X]$ or $\mu$)**

- **Definition:** The theoretical long-term average of a random variable.

- **Formula (Discrete):**

  $$E[X] = \sum x \cdot P(X=x)$$

  - It is a **weighted sum** of all possible outcomes, weighted by their probabilities .

- **Distinction:** Expectation is a population constant (theoretical center). It is different from the **sample mean**, which is an average calculated from a specific dataset .

- **Example (Casino Game):**

  - Losing $1 (prob 0.6), Winning $1 (prob 0.3), Winning $2 (prob 0.08), Winning $3 (prob 0.02).
  - $E[X] = (-1)(0.6) + (1)(0.3) + (2)(0.08) + (3)(0.02) = -0.08$.
  - *Interpretation:* On average, you lose 8 cents per game over the long run .

#### **2. Variance ($Var(X)$ or $\sigma^2$)**

- **Definition:** Measures the magnitude of fluctuation or dispersion around the mean.

- **Concept:** Average of the **squared differences** from the mean.

  $$Var(X) = E[(X - \mu)^2]$$

  - We square the difference because simple differences sum to zero .

- **Shortcut Formula:**

  $$Var(X) = E[X^2] - (E[X])^2$$

  - Derived by expanding the quadratic term inside the expectation .

- **Properties:**

  - $Var(C) = 0$ (Variance of a constant is 0).
  - $Var(aX + b) = a^2 Var(X)$ (Constants pull out as squares; shifts do not affect variance) .

- **Example (Risk Measurement):** Two lottery games (Paulina vs. Keno) had the same Expected Value (-0.25) but vastly different variances (55 vs 1.68). The high variance game represents higher risk .

#### **3. Covariance & Standardization**

- **Covariance:** Measures how two variables move together: $E[(X-\mu_x)(Y-\mu_y)]$ .

- **Standardization (Z-score):**

  $$Z = \frac{X - \mu}{\sigma}$$

  - Used to convert any dataset to have Mean=0 and Std Dev=1. Essential for preprocessing data for neural networks .



# 1/26 Lecture 4

### **I. Introduction to Predictive Modeling**

**1. Statistical Learning vs. Machine Learning**

- **Origins:** Machine Learning (ML) originated from Artificial Intelligence (AI), while Statistical Learning (SL) originated from Statistics .
- **Convergence:** Nowadays, the fields have essentially converged and are often treated as identical.
- **Distinctions in Focus:**
  - **Machine Learning:** Focuses on large-scale predictions and prediction accuracy (e.g., neural networks) .
  - **Statistical Learning:** Focuses on statistical inference, interpretability, and the precision of the prediction (e.g., understanding the relationship between input $X$ and output $Y$) .

**2. Historical Timeline**

- **19th Century:** **Least Squares Method** (Linear Regression) was developed for quantitative predictions .
- **1930s-1940s:** **Linear Discriminant Analysis (LDA)** and **Logistic Regression** were developed to handle categorical outputs (Classification) .
- **1970s:** **Generalized Linear Models (GLM)** created a framework accommodating both regression and classification .
- **1980s:** **Decision Trees** and **Neural Networks** emerged (though Neural Networks had limited application initially) .
- **1990s:** **Support Vector Machines (SVM)** were proposed for classification .

------

### **II. Core Terminology & Problem Types**

**1. Variable Definitions**

- **$Y$ (Output):** Referred to as the **Response variable**, Dependent variable, or Target value .
- **$X$ (Input):** Referred to as **Predictors**, Independent variables, Regressors, or **Features** (common in CS) .

**2. Types of Predictive Problems**

- **Regression (Quantitative Prediction):**
  - The model output is a numerical value (e.g., stock price, blood pressure, salary) .
- **Classification:**
  - The model output is a categorical value or class likelihood (e.g., Spam vs. No Spam, Digit 0-9, Cancer vs. No Cancer) .

**3. Real-world Examples**

- **Prostate Cancer Risk:** Classification (Cancer/No Cancer) based on health metrics .
- **Voice Recognition:** Classification (identifying the speaker) from voice frequency data .
- **Spam Detection:** Classification (Spam/No Spam) based on email content .
- **Handwritten Digit Recognition:** Classification (0-9) from image scans .
- **Salary Prediction:** Regression (Income level) based on demographics .
- **Traffic Volume:** Regression (Number of cars) to manage congestion .

------

### **III. Learning Paradigms**

**1. Supervised Learning**

- **Definition:** The dataset contains both the Input ($X$) and the observed Output ($Y$) .
- **Goal:** To find optimal coefficients (e.g., $\beta_0, \beta_1$) such that the model output matches the observed target $Y$ closely .
- **Why "Supervised"?** The observed response variable ($Y$) acts as a "benchmark" or target to supervise the learning/estimation process .
- **Training Data:** Must contain pairs of observations ($x_i, y_i$) .

**2. Unsupervised Learning**

- **Definition:** The dataset contains *only* Inputs ($X$), with no corresponding Output/Target ($Y$) .
- **Goal:** Since prediction is impossible without a target, the goal is to identify **patterns** or **clusters** based on feature similarity .
- **Application:** Clustering (grouping similar observations) often serves as a pre-processing step .

------

### **IV. Exploratory Data Analysis (EDA)**

Before choosing a model, it is crucial to understand the basic relationships in the data.

- **Scatter Plots:** Used to visualize relationships between predictors and response.
  - *Example (Wage Data):*
    - **Wage vs. Age:** Shows a non-linear curve (salary peaks at ~40-60 years old, then stagnates/drops) .
    - **Wage vs. Year:** Shows a slight linear increase (inflation) .
    - **Wage vs. Education:** Shows a stepwise increase with higher education levels .
- **Box Plots:** Used for categorical or time-series groupings.
  - *Example (Stock Market):* Using past days' returns (lagged data) to group "Up" vs. "Down" days. If the medians of the box plots are identical, it suggests the past data provides no predictive power (50/50 chance) .

------

### **V. The Theoretical Model**

**1. The Equation**

The relationship between input and output is modeled as:

$$Y = f(X) + \epsilon$$

- **$Y$:** The observed response variable .
- **$f(X)$:** The **deterministic part** (the model). This represents the systematic information that $X$ provides about $Y$ .
- **$\epsilon$ (Epsilon):** The **random noise** (error). This part cannot be modeled by any technique .
  - *Assumption:* $\epsilon$ is usually assumed to follow a Normal distribution with mean 0 and variance $\sigma^2$ ($\epsilon \sim N(0, \sigma^2)$) .

**2. Interpretation of the Model**

By taking the expectation on both sides:

$$E[Y|X] = f(X)$$

- **Meaning:** The model output $f(x)$ represents the **long-term average** (expectation) of the response variable $Y$ at a specific value of $X$ .
- **Why predictions don't match observations exactly:** The model predicts the *mean*. An actual observation ($Y$) includes random noise ($\epsilon$), so the model output ($f(X)$) will almost never equal a single specific observed data point .

------

### **VI. Purpose of Modeling: Prediction vs. Inference**

**1. Prediction**

- **Goal:** Focus solely on the accuracy of the output $\hat{Y}$. The relationship between variables matters less than the result.
- **Example (Direct Marketing):** A company wants to know *who* will respond positively to an ad. They don't care *why*; they just want to send mail only to those predicted to respond .

**2. Statistical Inference**

- **Goal:** Understand the relationship between predictors and response.
- **Key Questions:**
  - Which predictors are associated with the response? (e.g., Does Newspaper advertising actually impact Sales?) .
  - What is the relationship? (Positive/Negative/Magnitude) .
- **Example (Real Estate):**
  - *Inference:* "How much extra is a house worth if it has a river view?" (Isolating the effect of one variable) .
  - *Prediction:* "Is this specific house undervalued?" (Comparing model price vs. market price) .

**3. Model Selection Philosophy**

- **Simpler is often better:** Do not assume complex models (like Neural Networks) are always superior. For small datasets, simple regression often performs as well or better and is faster.
- **Estimation Methods:** Future lectures will cover methods like Least Squares, Maximum Likelihood Estimation (MLE), and Gradient Descent .



# 1/28 Lecture 5

# **ISE 529 Lecture Notes: Model Estimation, Bias-Variance Trade-off, and Model Assessment**

**Lecture Date:** Jan 28, 2026 | **Topic:** Predictive Modeling & Assessment

------

## **1. Introduction to Model Estimation**

The lecture builds upon the previous topic of *why* we estimate prediction models (prediction vs. inference). The focus now shifts to **how** to estimate these models.

### **Key Estimation Methods**

The course introduces several algorithms/procedures for estimating predictive models:

- **Least Squares:** The first algorithm introduced; a regression technique dating back to the 19th century. Used to find optimal parameters for linear models.
- **Maximum Likelihood Estimation (MLE):** A powerful, widely used method for estimating various model types.
- **Gradient Descent:** Used primarily for estimating Neural Networks.
- **Entropy Methods:** Used for estimating Decision Trees.
- **Kernel Methods:** Used for Support Vector Machines (SVM) in classification.

### **The Learning Process**

- **Goal:** Find optimal model parameters so the model output ($\hat{f}(X)$) is as close as possible to the observed response ($Y$).
- **Training Data:** The dataset used to estimate the model (or "train" it). Contains observed values for both the response variable and predictors.
- **Terminology:** "Model estimation" and "learning process" are interchangeable terms.

------

## **2. Parametric vs. Non-Parametric Models**

Models are classified into two main streams based on their structure and estimation approach.

### **A. Parametric Models**

A two-step approach:

1. **Make an Assumption:** Assume the functional form of the relationship (e.g., linear).
   - *Example:* Linear model $f(X) = \beta_0 + \beta_1X_1 + \dots + \beta_pX_p$.
   - The problem boils down to estimating the coefficients ($\beta$).
2. **Estimate Parameters:** Use an algorithm (like **Least Squares**) to fit the data and find the coefficients.

- **Pros:** Simpler, easier to interpret (high interpretability).
- **Cons:** The assumed model rarely matches the unknown true underlying model $f$. If the assumption is wrong, the estimation will be poor.

### **B. Non-Parametric Models**

- **Definition:** Do not assume a specific functional form with fixed parameters. They are "free form".
- **Example:** **Spline Models** (curvy planes) or **Moving Average Filters**.
  - *Moving Average Filter:* Uses a "window" or bandwidth (parameter $q$) to average neighboring points to predict a value at time $t$.
  - As $q$ increases, more neighbors are averaged.
- **Pros:** Can fit data much better and capture complex, "curvy" relationships.
- **Cons:**
  - Requires a very large dataset to estimate accurately.
  - Prone to **Overfitting**: The model follows the training data (and noise) too closely, leading to poor performance on new data.

------

## **3. Interpretability vs. Flexibility**

There is a fundamental trade-off between how flexible a model is and how interpretable it is.

- **Flexibility:** The ability of a model to fit complex data shapes (e.g., a wiggly curve vs. a straight line).
  - *High Flexibility:* Neural Networks, Support Vector Machines (SVM), Splines.
  - *Low Flexibility:* Linear Regression, Lasso.
- **The Trade-off:** As flexibility increases, interpretability decreases.
  - *Linear Regression:* Highly interpretable (you understand the relationship between each predictor and the response).
  - *Neural Networks:* "Black box" models; impossible to interpret specific weight matrices.

### **Selection Rule (Parsimony Principle)**

- **Inference Goal:** If the goal is to understand relationships (inference), choose **simple, less flexible models** (e.g., Linear Regression).
- **Prediction Goal:** If the goal is purely prediction accuracy, you *might* choose a **flexible model**, but not always. Surprisingly, simple models can sometimes outperform flexible ones because flexible models overfit.
- **Parsimony Principle:** If a simple model and a complex model perform similarly, **always choose the simpler model**.

------

## **4. Classification vs. Regression**

Model selection also depends on the type of response variable ($Y$).

- **Quantitative (Numerical) Response:** Called a **Regression** problem. Use Linear Regression, etc..
- **Qualitative (Categorical) Response:** Called a **Classification** problem. Use Logistic Regression, etc..
- *Note:* The type of *predictor* ($X$) does not determine the model type, only the response variable does.

------

## **5. Assessing Model Accuracy**

> "All models are wrong, but some are useful." — George Box 

- *Meaning:* We never know the true underlying random process. We only approximate it. If the approximation predicts well, it is "useful".

### **Measuring Performance: Mean Squared Error (MSE)**

The standard metric for assessing model performance is the **Mean Squared Error (MSE)**.

$$MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{f}(x_i))^2$$

- $y_i$: Observed value
- $\hat{f}(x_i)$: Model prediction
- Measures the average squared difference between observation and prediction.

### **Training MSE vs. Test MSE**

1. **Training MSE:** Calculated using the same data used to train the model.
   - *Property:* Usually small because the model is designed to minimize this error.
   - *Flaw:* A low training MSE does not guarantee a good model; it typically decreases monotonically as flexibility increases .
2. **Test MSE:** Calculated using a **new, unseen dataset** ($x_0, y_0$).
   - *Purpose:* The true measure of prediction accuracy.
   - *Property:* Follows a **U-shaped curve** when plotted against model flexibility.

### **The U-Shape Pattern (Bias-Variance Trade-off)**

- **Low Flexibility (Simple Models):** High Bias, Low Variance. Test MSE is high.
- **Medium Flexibility:** Optimal balance. Test MSE is minimized (bottom of the U).
- **High Flexibility (Complex Models):** Low Bias, High Variance. Test MSE rises again due to **overfitting** (modeling the noise).

------

## **6. Bias-Variance Trade-off Theorem**

The most important theorem in the course. It mathematically decomposes the expected Test MSE into three components.

$$E(y_0 - \hat{f}(x_0))^2 = Var(\hat{f}(x_0)) + [Bias(\hat{f}(x_0))]^2 + Var(\epsilon)$$

### **The Components**

1. **Variance of the Model ($Var(\hat{f}(x_0))$):**
   - How much the model function $\hat{f}$ would change if estimated with a different training dataset.
   - Flexible models have **high variance** (they change a lot with new data).
2. **Squared Bias ($[Bias(\hat{f}(x_0))]^2$):**
   - The error introduced by approximating a real-life problem with a simplified model.
   - $Bias = E[\hat{f}(x_0)] - f(x_0)$ (Difference between expected model output and true model).
   - Simple models (linear) have **high bias**. Flexible models have **low bias**.
3. **Irreducible Error ($Var(\epsilon)$):**
   - The variance of the error term (noise) $\epsilon$.
   - This is system error inherent to the data; it cannot be reduced by any model.

### **Derivation Logic (Brief)**

- Observation $Y = f(X) + \epsilon$.
- We want to minimize $E[(Y - \hat{f}(X))^2]$.
- The expansion involves:
  - $f(x)$ (True model)
  - $\hat{f}(x)$ (Estimated model)
  - $\epsilon$ (Noise)
- The cross-terms involving $\epsilon$ often cancel out because $E[\epsilon] = 0$.
- **Homework Hint:** You will need to prove the decomposition of these terms in the homework.

### **Key Takeaway**

- To minimize Test MSE, you must minimize the sum of Variance and Squared Bias.
- **Trade-off:** You cannot minimize both simultaneously. Increasing flexibility reduces bias but increases variance. You must find the "sweet spot" (the bottom of the U-curve).

------

## **7. Statistical Review (Bias in Estimators)**

A brief review of statistical bias was provided to support the theorem.

- **Unbiased Estimator:** An estimator (formula) is unbiased if its expected value equals the true population parameter: $E[\hat{\theta}] = \theta$.
- **Sample Mean ($\bar{x}$):** Proven to be an unbiased estimator of population mean $\mu$.
- **Sample Variance ($S^2$):** Proven to be an unbiased estimator of population variance $\sigma^2$ (due to the $n-1$ denominator).

------

**Next Class:** Will continue proving the Bias-Variance theorem and further discussing how to choose the best model.



# 2/2 Lecture 6

**ISE 529 Lecture Cheatsheet: Bias-Variance Tradeoff, K-NN, and Linear Regression**

**Date:** February 2, 2026

---

### **I. The Bias-Variance Trade-off Theorem**

This theorem is fundamental for selecting the best model for prediction. The golden indicator used to measure the performance of model prediction is the **Test MSE (Mean Squared Error)**.

**The Test MSE Formula:**
The Test MSE can be decomposed into three distinct components:

1. **Variance of the Model:** The variance introduced by the specific methodology chosen.


2. **Bias of the Model:** The error introduced by approximating a real-life problem with a simpler model.


3. **Variance of the Data (Irreducible Error):** The inherent noise or variation in the data itself.

**Detailed Breakdown of Components:**

* **Variance of the Model:**

  * *Calculation:* Expectation of the squared difference between a single estimated model's output ($\hat{f}(x_0)$) and the theoretical long-term average model output ($E[\hat{f}(x_0)]$).
  
  
    * *Concept:* Models are estimated based on one sample data set. If you drew multiple samples, you would get different models. This variability is the model's variance.
  
  
    * *Rule of Thumb:* More flexible/complex methods (e.g., neural networks) generally have **higher variance** because small changes in training data result in large changes in the model output.
  
* **Bias of the Model:**


    * *Calculation:* Difference between the underlying true model ($f(x)$) and the theoretical expected value of the chosen method's model ($E[\hat{f}(x)]$), squared.


    * *Concept:* The underlying true model is invisible. No method will perfectly match it.


    * *Rule of Thumb:* More flexible methods generally result in **less bias** because they fit the training data better. However, fitting the data *too* well can capture noise, leading to overfitting.



* **Variance of the Data (Irreducible Error - $\epsilon$):**


    * *Calculation:* Expectation of the squared difference between the observed response ($y_0$) and the true model's output ($f(x_0)$).


    * *Concept:* This error cannot be reduced regardless of the chosen method. It often represents unmeasured but important predictor variables.



**Visualizing the Trade-off:**
When plotted against model flexibility, the Test MSE curve is the sum of three curves:

* **Blue Curve (Bias):** Decreases as flexibility increases.


* 
**Orange Curve (Variance):** Increases as flexibility increases.


* 
**Gray Line (Irreducible Error):** Remains constant.


* **Red Curve (Test MSE):** U-shaped. **Goal:** Choose the flexibility level that minimizes the Test MSE (the lowest point on the red curve).

---

### **II. Classification and Error Rates**

When the response variable is qualitative (e.g., Yes/No, Dog/Cat), MSE is not appropriate. Instead, use Error Rates.

**Training / Test Error Rate:**

* *Formula:* Relies on an **Indicator Function ($I$)**.


* *Indicator Function logic:* Outputs 1 if the predicted class ($\hat{y}_i$) does not equal the observed class ($y_i$) (a misclassification); outputs 0 if they match.


* *Calculation:* Sum the misclassifications and divide by the total number of observations ($n$).


* Training Error Rate is equivalent to Training MSE; Test Error Rate is equivalent to Test MSE.

---

## Slide 03 Linear Regression (I)

### **III. K-Nearest Neighbors (K-NN) Classifier**

The Bayes Classifier requires knowing the probability distributions of both input and output variables, which is often impossible . K-NN is a simple method to approximate the Bayes Classifier.

**How K-NN Works:**

1. 
**Choose $K$:** Select the number of nearest neighborhood points to consider (e.g., $K=3$).


2. **Calculate Distance:** Find the $K$ closest points in the training dataset to the new observation. Distance is typically calculated using the **Euclidean distance formula** for vectors.


3. **Approximate Probability:** Calculate the proportion of the $K$ neighbors that belong to a specific class.


4. **Classify:** Assign the new observation to the class with the highest estimated probability (threshold typically $> 0.5$).

**Flexibility in K-NN:**

* **$K=1$:** The most flexible, highly variable model. Decision is based entirely on the single closest point.


* **High $K$ (e.g., $K=100$):** The least flexible, most rigid model. The decision boundary becomes smoother, almost linear.


* *Note:* In flexibility graphs, the x-axis is often $1/K$, meaning flexibility increases as you move right. Choose $K$ that minimizes the Test Error Rate (e.g., $K=10$).

---

### **IV. Simple Linear Regression**

Linear regression checks model adequacy and determines correlation between a predictor and response variable.

**The Model:**

* 
  **Equation:** $Y_i = \beta_0 + \beta_1X_i + \epsilon_i$.
  
  
    * 
      $Y$: Response / Dependent Variable.
  
  
    * 
      $X$: Predictor / Independent Variable.
  
  
    * 
      $\beta_0$: Intercept.
  
  
    * 
      $\beta_1$: Slope (Coefficient representing correlation).
  
  
    * 
      $\epsilon$: Random noise/error (assumed to follow Normal Distribution, mean=0, variance=$\sigma^2$).
  
* **Expectation:** Taking the expectation of the model yields $E[Y|X] = \beta_0 + \beta_1X$. The model output represents the long-term average (expectation) of the observed response given an input.

**Method of Least Squares:**
The goal is to find values for $\beta_0$ and $\beta_1$ that minimize the distance between the model output ($\hat{y}_i$) and the observed values ($y_i$).

* **Objective Function (SSE):** Minimize the Sum of Squared Errors (SSE): $\sum (y_i - \hat{y}_i)^2$.


* 
**Optimization:** Take the first-order partial derivatives of the objective function with respect to $\beta_0$ and $\beta_1$, and set them to 0.


* This results in a system of equations called **Normal Equations**.


* **Solutions:**


    * 
      $\hat{\beta}_1 = S_{xy} / S_{xx}$.
    
      * $S_{xx}$ is equivalent to variance of X; $S_{xy}$ is equivalent to covariance of X and Y.
    
    * 
      $\hat{\beta}_0 = \bar{y} - \hat{\beta}_1\bar{x}$ (where $\bar{y}$ and $\bar{x}$ are sample means).


**Estimating Variance ($\sigma^2$):**

* 
  $\sigma^2 = SSE / (n - p)$.
  
  
    * 
      $n$ = sample size.
  
  
    * 
      $p$ = number of parameters estimated (for simple linear regression, $p=2$ because we estimate $\beta_0$ and $\beta_1$).
  


---

### **V. Hypothesis Testing for Regression Coefficients**

Hypothesis testing is used to verify if the estimated model is statistically significant.

**The 4 Steps of Hypothesis Testing:**

1. 
    **State the Hypothesis ($H_0$ and $H_1$):** 
    
    
      * *Null ($H_0$):* Assume the theoretical parameter equals a specific value (e.g., $H_0: \beta_1 = 0$). If $\beta_1 = 0$, it means there is no relationship between X and Y.
    
    
      * *Alternative ($H_1$):* Assume it does not equal that value (e.g., $H_1: \beta_1 \neq 0$).
    
2. **Calculate the Test Statistic ($t$):** 


     * Formula: $t = (\text{Estimated Value} - \text{Assumed Value}) / \text{Standard Deviation of the Estimate}$.
    
       * $$T = \frac{\bar{X} - \mu}{S/\sqrt{n}}$$
    
     * For slope: $t = (\hat{\beta}_1 - 0) / SE(\hat{\beta}_1)$.


     * This statistic follows a $t$-distribution with $n-2$ degrees of freedom.


3. **Find the Critical Value:** 
     * Given a significance level $\alpha$ (e.g., $0.05$ or $0.01$) and degrees of freedom, use a $t$-distribution table to find the critical boundary values that correspond to the probability $1 - \alpha$.


4. **Compare and Conclude:** 


     * If the calculated $t$-statistic falls **outside** the critical value boundaries (i.e., it is greater than the positive critical value or less than the negative critical value), the probability model is broken.


     * **Conclusion:** **Reject $H_0$**. This means the data does not support the assumption that $\beta_1 = 0$. Therefore, $\hat{\beta}_1 \neq 0$, indicating a statistically meaningful relationship exists between X and Y.


     * If the $t$-statistic falls **inside** the boundaries, you **fail to reject $H_0$**, meaning the assumption holds.




# 2/4 Lecture 6

### **1. Hypothesis Testing for Regression Coefficients (t-test)**

Hypothesis testing is used to determine if an estimated linear regression model is statistically significant by evaluating its coefficients .

* 
**Step 1: Make Assumptions.** Establish a null hypothesis ($H_0$) assuming the population parameter equals a specific value (e.g., $\beta_1 = 0$), and an alternative hypothesis ($H_1$) assuming it does not .


* 
**Step 2: Calculate the t-statistic.** Standardize the estimate by dividing the difference between the estimated value and the assumed value by the standard deviation (e.g., $t = (\hat{\beta}_1 - 0) / SE(\hat{\beta}_1)$) .


* **Step 3: Find Critical Value.** Choose a level of significance ($\alpha$, usually 0.05) to determine the probability model, and look up the critical boundaries in a t-distribution table . 
* **Step 4: Compare and Conclude.** If the calculated t-statistic falls outside the interval of the critical values, the probability model is broken, and you must reject the null hypothesis .
* **Interpretation:** Rejecting $H_0$ ($\beta_1 = 0$) means $\hat{\beta}_1 \neq 0$, concluding that the model is meaningful and a true relationship exists between the predictor ($x$) and response ($y$) .

---

### **2. Confidence Intervals**

Because an estimated regression line is a random model based on a single sample, point estimates are insufficient on their own . Confidence intervals provide a theoretical lower and upper bound for coefficients and predictions .

* **Calculation Formula:** The interval is calculated as the estimated value plus or minus the critical value multiplied by the standard deviation .


* **Fitted Value vs. Prediction:** The model output for training data is called a "fitted value," whereas the output for future, unseen data is a "prediction" .


* 
**Interval Width:** The confidence interval for a future prediction is *always wider* than the interval for a fitted value .


* **Reasoning:** Prediction intervals must account for the baseline model error *plus* the additional, unknown error ($\sigma^2$) associated with future observations .

---

### **3. Checking Model Adequacy (4 Methods)**

Once a model is estimated, its adequacy must be verified using one of four primary methods .

**Method A: The t-test**

* Checks the significance of every single individual coefficient in the model.

**Method B: ANOVA and R-Squared**

* 
**Total Variation:** The Sum of Squares Total ($SST$) measures the variation of all observed response variables from the data's center point ($\bar{y}$) .


* **Decomposition:** $SST = SSR + SSE$. 
* **SSR (Regression Sum of Squares):** The portion of total variation successfully explained by the model .


* **SSE (Error Sum of Squares):** The remaining random variation (residuals) that the model cannot explain .


* 
**R-Squared ($R^2$):** Known as the coefficient of determination, calculated as $SSR / SST$.


* **Interpretation:** $R^2$ represents the percentage of total variation explained by the model; a higher value indicates a better-performing model .

**Method C: The F-test (ANOVA Table)**

* Unlike the t-test, the F-test checks if the *overall* model is statistically significant.


* The null hypothesis ($H_0$) assumes all slope coefficients simultaneously equal zero .


* The alternative hypothesis ($H_1$) assumes *at least one* coefficient does not equal zero, though it cannot specify which one .


* The F-statistic is calculated by dividing the Mean Square Regression ($MSR$) by the Mean Square Error ($MSE$) .

| Source | Sum of Squares | Degree of Freedom | Mean Square | F-Statistic |
| --- | --- | --- | --- | --- |
| Regression | $SSR$ | $k$ | $MSR = SSR / k$ | $F = MSR / MSE$ |
| Error | $SSE$ | $n - p$ | $MSE = SSE / (n-p)$ |  |
| Total | $SST$ | $n - 1$ |  |  |

Table notes: The first row plus the second row equals the total row for both Sum of Squares and Degrees of Freedom . The number of predictors is $k$, and the total number of coefficients is $p$ ($p = k + 1$) .

**Method D: Residual Analysis**

* Residuals (the difference between observed values and model outputs) should act as pure noise, being independently and identically distributed (i.i.d.) and following a normal distribution .


* Use a QQ plot to verify normal distribution; the residuals should fall along a straight line . * Use a scatter plot to visualize residuals against predictors; any visible pattern indicates the model failed to capture important information .

---

### **4. Correlation**

* Correlation measures the rhythm and directional relationship (positive or negative) between two random variables .


* It is calculated by dividing the covariance by the standard deviations of both variables .


* Because standard deviations cancel out the original units, correlation is a unitless indicator .


* In simple linear regression, the estimated slope coefficient ($\hat{\beta}_1$) is effectively the standardized ratio of this correlation.

---

### **5. Maximum Likelihood Estimation (MLE)**

* MLE is a more powerful estimation method than Least Squares because it can be applied to almost any type of model, not just regression.


* It assumes the response variable follows a specific probability distribution, such as a normal distribution.


* The "likelihood function" calculates the total joint probability of observing the specific dataset by multiplying individual observation likelihoods together.


* The goal of MLE is to find the parameter values ($\theta$) that maximize this joint probability function.


* A log-likelihood function is typically used to convert multiplication into summation, making it easier to take derivatives and solve.


* For simple linear regression, MLE yields the exact same slope and intercept coefficient formulas as the Least Squares method.


* However, MLE results in a *biased* formula for the variance ($\sigma^2$), dividing the error by $n$ instead of $n - 2$.



# 2/9 Lecture 7

## Slide 05. Multiple Linear Regresssion

### 1. Multiple Linear Regression Model Foundation

* The model aims to explain a response variable using multiple predictors instead of just one.


* The theoretical equation is $y = \beta_0 + \beta_1 x_1 + \dots + \beta_k x_k + \epsilon$.


* There are $k$ predictors in the model.


* Model estimation requires finding values for the intercept ($\beta_0$) and all coefficients ($\beta_1$ to $\beta_k$).


* In matrix form, the dataset involves a column of observed response variables ($Y$) and a matrix of predictors ($X$).


* The $X$ matrix requires an artificially added first column of 1s to accommodate the intercept $\beta_0$.


* The compact matrix representation of the model is $Y = X\beta + \epsilon$.

### 2. Parameter Estimation (Least Squares Method)

* The objective is to minimize the Sum of Squared Errors (SSE) between the observed responses and the model outputs.


* The error function is $L = \sum (y_i - \hat{y}_i)^2$.


* Minimization involves taking the first-order partial derivatives of the objective function for every $\beta$ and setting them to zero.


* This creates a system of $k+1$ normal equations to solve for the coefficients.


* A key property from the first normal equation is that the sum of observed values equals the sum of model outputs ($\sum y_i = \sum \hat{y}_i$).


* In matrix notation, the objective function to minimize is $(Y - X\beta)^T(Y - X\beta)$.


* The derived matrix solution for the coefficients is $\hat{\beta} = (X^T X)^{-1} X^T Y$.


* The term $X^T X$ represents the covariance matrix of the inputs.


* The error variance estimate is calculated as $\hat{\sigma}^2 = SSE / (n - p)$.


* The value $p$ equals $k + 1$ (the total number of estimated coefficients, including the intercept).

### 3. Hypothesis Testing & Adequacy

* 
**F-Test (Overall Regression):** Checks the adequacy of the entire model.


* The null hypothesis assumes all predictor coefficients equal zero ($\beta_1 = \beta_2 = \dots = \beta_k = 0$).


* The alternative hypothesis states that at least one coefficient does not equal zero.


* The F-statistic is calculated as $F = MSR / MSE$.


* Rejecting the null hypothesis means at least one predictor has a significant relationship with the response variable.


* 
**T-Test (Marginal Test):** Used to check if an individual predictor coefficient is statistically significant.


* The t-statistic is the estimated coefficient divided by its standard error ($t = \hat{\beta}_j / se(\hat{\beta}_j)$).


* Standard errors are derived using the major diagonal elements of the inverse covariance matrix $C = (X^T X)^{-1}$.


* The variance for a specific beta is $\sigma^2 \times C_{jj}$.


* **ANOVA Table Breakdown:** Total Sum of Squares (SST) equals Regression Sum of Squares (SSR) plus Error Sum of Squares (SSE).


* 
$SST = Y^T Y - n\bar{y}^2$.


* 
$SSR = \hat{\beta}^T X^T Y - n\bar{y}^2$.


* 
$SSE = Y^T Y - \hat{\beta}^T X^T Y$.

### 4. Confidence Intervals

* The confidence interval for a coefficient is estimated by taking the parameter estimate $\pm$ the critical value multiplied by the standard error.


* Estimating the confidence interval for the fitted response ($\hat{y}$) requires calculating the variance of the model output.


* The variance calculation uses a quadratic form involving the $C$ matrix.


* The prediction interval for a new observation is wider than the confidence interval for the fitted mean.


* The prediction interval variance is greater by exactly one $\sigma^2$.

### 5. R-Squared vs. Adjusted R-Squared

* Standard $R^2$ represents the percentage of total variation in the response variable explained by the predictors.


* Adding any predictor, even an irrelevant one, will artificially increase standard $R^2$ and cause overfitting.


* Adjusted $R^2$ is a modified formula that accounts for the model's degrees of freedom.


* Adjusted $R^2$ penalizes the introduction of unnecessary variables as it increases the model size ($p$).

### 6. Residual Analysis

* Residuals are assumed to follow a normal distribution.


* Standardized residuals are calculated by taking the absolute residual minus zero, divided by the square root of MSE.


* A Q-Q plot is used to verify the normality assumption by checking if points fall along a straight line. * Scatterplots of residuals versus fitted values or predictors help identify hidden patterns.


* A visible pattern in the residual plot indicates an inadequate model that is failing to capture a specific relationship (e.g., non-linearity).

### 7. Advanced Regression Considerations

* **Interaction Effects:** Captures the synergy between two variables by introducing their product (e.g., $x_1 \times x_2$) as a brand new predictor feature.


* If an interaction term is kept in the model because it is significant, the individual main effects must also be kept, even if their isolated p-values are not significant.


* **Polynomial Regression:** Uses a linear model to capture non-linear (curved) relationships by raising an existing predictor to a power, such as $x^2$.


* Polynomial regression remains "linear" because the estimated coefficients ($\beta$) themselves remain linear.


* 
**Categorical Variables:** Handled by converting categories into dummy variables containing values of 0 or 1.


* The model requires creating one fewer dummy variable than the total number of categories available.


* 
**Extra Sum of Squares Method:** Used to select important variables by testing if an entire sub-group of predictors is significant.


* This method compares the SSR of the full model against the SSR of a reduced model to compute an F-statistic.

# **2/11 Lecture 8**

## ISE 529 Lecture Cheatsheet: Variable Selection and Logistic Regression

### Part 1: Variable Selection in Multiple Linear Regression

When working with large datasets containing many predictors, it is crucial to select only the most important variables rather than building a regression model with all of them.

**Five Key Indicators for Model Selection**

* 
**AIC (Akaike Information Criterion):** Uses log-likelihood with a negative sign, meaning the smaller the AIC value, the better the model. It adds a penalty term of $2p$ (where $p$ is the model size/number of predictors) to penalize unnecessarily large models and favor compact ones.


* 
**BIC (Bayesian Information Criterion):** A more powerful indicator similar to AIC, but it uses a penalty term of $p \times \log(n)$, where $n$ is the sample size. Lower BIC indicates a better model.


* **Mallows's $C_p$:** Calculated using the residual sum of squares from the evaluated model divided by the variance ($\sigma^2$) from the full model. The guiding principle is to choose a model where the $C_p$ value is close to the model size $p$.


* 
**Adjusted $R^2$:** An adjusted version of the coefficient of determination that helps overcome overfitting problems to some extent.


* **PRESS (Predicted Residual Error Sum of Squares):** Uses the leave-one-out cross-validation method. The dataset is split so that $n-1$ observations train the model, and the single remaining observation tests it, calculating the squared difference of the prediction. A shortcut formula allows you to calculate PRESS by estimating the full model only once using the "hat matrix" ($H = X(X^T X)^{-1}X^T$), where smaller PRESS values indicate a better model.

**Three Methods for Selecting Variables**

* 
**All Possible Regression:** Estimates every possible model combination ($2^p$ models). This is feasible for a small number of predictors (e.g., 5 predictors yield 32 models) but impossible for large datasets (e.g., 40 predictors).


* 
**Forward Selection:** Begins with a null model containing zero predictors. Predictors are added one at a time, and their significance (p-value) is checked to determine if they should be kept.


* **Backward Selection (Elimination):** Starts with the full model containing all possible predictors. The predictor with the highest, most insignificant p-value (e.g., $> 0.05$) is removed, and the model is re-estimated until only significant variables remain.

---

### Part 2: Multicollinearity

* Multicollinearity occurs when two or more predictors in a linear regression model have a very strong correlation with each other.


* If strong multicollinearity is present, the estimated coefficients become non-unique, unreliable, and unstable.


* It is measured using the **VIF (Variance Inflation Factor)**, calculated as $\frac{1}{1 - R_j^2}$.


* 
$R_j^2$ is found by regressing the predictor $X_j$ against all other predictors to see how much of its variation they explain.


* If a predictor's VIF is greater than 5 (strict) or 10 (loose), it indicates a problem and the variable should likely be removed.

---

# Slide 05: Classification (I)

### Part 3: Logistic Regression for Classification

* Classification models always output a probability indicating whether an input belongs to a certain class.


* Logistic regression assumes the response variable follows a Bernoulli distribution, which is used for binary outcomes (1 for success, 0 for failure).


* A standard linear regression model cannot be used because its output maps from $-\infty$ to $\infty$, while probabilities must strictly fall between 0 and 1.


* To solve this, the model uses the **Odds Ratio** ($\frac{\pi}{1 - \pi}$), which has a range from 0 to $\infty$.


* By taking the log of the odds ratio (log-odds), the range becomes $-\infty$ to $\infty$, allowing it to perfectly match the linear combination equation on the right-hand side.


* Isolating the probability ($\pi$) results in the final logistic function: $\pi = \frac{e^{\text{linear output}}}{1 + e^{\text{linear output}}}$.


* 
**Decision Rule:** By default, 0.5 is used as the comparative threshold; if the output probability is $> 0.5$, the input is assigned to class 1, otherwise to class 0.


* Visualizing a single-predictor model creates an "S-curve" graph, where the horizontal axis is the input $X$ and the vertical axis is the probability from 0 to 1.


* If the model assigns a probability $> 0.5$ but the real observed data falls into class 0, this is a misclassification.


* The **Misclassification Error Rate** is calculated by dividing the total number of misclassified points by the total number of observations.

---

### Part 4: Estimating and Evaluating Logistic Models

* Logistic regression models cannot be estimated using the least squares method.


* Instead, they are estimated using the **Maximum Likelihood Method**.


* The first step is constructing a joint probability likelihood function by multiplying the mass functions of all observed values.


* Taking the log of this function (log-likelihood) turns the multiplication into summation.


* Because $\beta$ cannot be isolated directly, numerical iteration via the **Newton-Raphson method** is used.


* Newton-Raphson updates the $\beta$ coefficients step-by-step by subtracting a gradient (calculated using the Jacobian vector and Hessian matrix) from the initial values until the log-likelihood improvement stops.


* To test if a logistic model is significant, a **Chi-Square test** is used instead of a t-test.


* The Chi-Square statistic compares the likelihood ratio of a full model against a reduced model (without a specific predictor).


* 
**Interpreting Coefficients:** If a variable's coefficient is positive, a one-unit increase in that variable increases the log-odds, resulting in a higher probability of the outcome occurring.


* Always perform sanity checks on the estimated model, as improper model specification can yield conflicting or illogical results (e.g., student status lowering default probability in a multivariate model but raising it in a univariate model).



# 2/18 Lecture 9

### ISE 529 Lecture Notes: Logistic Regression & Generative Classifiers

---

### 1. Data Formats for Logistic Regression

The lecture covers two mathematical formats for binary classification data that yield the exact same logistic regression model and coefficients .

* 
**Binary Data (Bernoulli Distribution):** The response variable is recorded as a single observation per row with only two possible outcomes, such as success or failure (often coded as 1 or 0) .


* 
**Binomial Data (Aggregated):** This format groups identical predictor variables together . The response variable represents the number of successes out of the total number of experimental trials for that group .


* **Python Implementation (`statsmodels`):** For binary data, the dependent variable `y` is a single column of 1s and 0s . For binomial data, `y` must be formatted as a two-column matrix containing the number of successes in the first column and the number of failures in the second column . Both methods utilize the `family=binomial` parameter within the GLM (Generalized Linear Model) function.

### 2. Maximum Likelihood Estimation (MLE)

Logistic regression models cannot be solved using a simple, closed-form equation to isolate beta coefficients like linear regression can .

* The model relies on the Maximum Likelihood Estimation method.


* The joint probability of observed values is transformed from a multiplication function into a summation by taking the log, creating the log-likelihood function .


* Numerical methods, specifically the Newton-Raphson method, are used to iteratively estimate the optimal beta values until the log-likelihood function is maximized .

### 3. Multinomial Logistic Regression

When a dataset contains more than two classes, standard binary logistic regression must be expanded .

* 
**Baseline Class Approach:** One class is established as the baseline. If there are $K$ classes, the model will output $K-1$ sets of beta coefficients to calculate probabilities .


* **Softmax Function:** An alternative mathematical formulation where no single class acts as a baseline . Every single class receives its own set of beta coefficients . This softmax format is frequently used in neural networks, such as CNNs .

### 4. Generative Models (Bayes Classifiers)

Logistic regression has vulnerabilities: it is unstable when classes are perfectly separated, struggles with very small sample sizes, and scaling to multiple classes can be complex . Generative models solve this by utilizing Bayes' Theorem .

* 
**Bayes' Theorem Application:** Instead of directly estimating the probability of a class given an input, these models flip the condition to calculate the probability of the input given the class .


* 
**Posterior Probability:** The model multiplies the prior probability (the historical probability of a class occurring) by the density function (the distribution of the input variables) to output the posterior probability .


* 
**Linear Discriminant Analysis (LDA):** This model assumes that predictor variables follow a Normal (Gaussian) distribution within every class . It also simplifies calculations by assuming that the variance (or covariance matrix) is identical across all classes .


* **Discriminant Function:** To avoid complex probability calculations, taking the log of the full model yields the discriminant function . The input observation is assigned to the class that generates the highest discriminant score . Due to the equal variance assumption, the resulting decision boundary is strictly linear .

### 5. Evaluating Performance: Confusion Matrix

Model accuracy is evaluated using a confusion matrix .

* **Major Diagonal:** Represents correct predictions by the model . Adding these values and dividing by the total sample size calculates the model's overall accuracy.


* **Minor Diagonal:** Represents the model's misclassifications . Adding these values and dividing by the total sample size determines the model's error rate.

### 6. Exam Preparation Notes

* The exam evaluates theoretical understanding; understanding the theory makes application a "piece of cake" .


* There will be no coding required on the exam .


* You must be able to read computer output tables and construct the logistic regression mathematical equations by hand .


* Be prepared to calculate the probability of an observation belonging to a certain class given the predictor values .



# 2/23 Lecture

### Linear Discriminant Analysis (LDA) Recap

* **Core Approach:** LDA is a linear classification model that calculates discriminant scores using Bayes' theorem.


* **Predictor Assumption:** It assumes that multiple predictors ($x_1, x_2, \dots, x_p$) follow a joint normal distribution.


* 
**Covariance Assumption:** The model implicitly assumes that the covariance matrix ($\Sigma$) is identical across all different classes.


* 
**Model Linearity:** The shared covariance matrix across the dataset is the specific reason why the resulting discriminant equation remains linear.


* **Prediction:** New inputs are plugged into the discriminant function to calculate scores, which can then be converted into probabilities to classify the input.

### Confusion Matrix & Performance Evaluation

* 
**Matrix Structure:** The columns represent the true observed classes, while the rows represent the model's predictions.


* 
**Correct Predictions:** Values along the major diagonal represent correct classifications, where the model output matches the true observations.


* 
**Misclassifications:** Values on the minor diagonal represent errors, such as False Positives and False Negatives.


* 
**Accuracy:** Calculated by summing the major diagonal values and dividing by the total number of samples.


* **Error Rate:** Calculated by summing the minor diagonal values and dividing by the total number of samples.


* 
**Sensitivity:** The percentage of true positives that are correctly identified by the model.


* 
**Specificity:** The percentage of true negatives that are correctly identified by the model.


* 
**Threshold Tuning:** You can adjust the probability threshold (e.g., changing 0.5 to 0.2) to purposely make the model stricter and reduce costly misclassifications, such as false negatives in banking loans.


* **ROC Curve:** Evaluates model performance visually; an ideal curve hugs the top-left corner, indicating a high true positive rate and a low false positive rate.

---

### Quadratic Discriminant Analysis (QDA)

* 
**Core Approach:** QDA is a non-linear model where the boundary between classes is a curve rather than a straight line.


* 
**Covariance Assumption:** Unlike LDA, QDA assumes that every individual class has its own distinct covariance matrix ($\Sigma_k$).


* 
**Mathematical Form:** The discriminant function contains a quadratic term to the power of two due to vector-matrix multiplication involving the distinct covariance matrices.


* 
**Parameter Cost:** Because it calculates separate covariance matrices, QDA requires estimating significantly more parameters than LDA.


* 
**Data Requirements:** QDA is highly flexible and requires a much larger dataset to properly estimate the parameters without overfitting.


* **Model Selection:** LDA performs better when classes share similar correlations, while QDA is superior when classes exhibit vastly different correlations.

---

### Naive Bayes Classifier

* 
**Core Philosophy:** The model simplifies complex joint probability calculations by making a "naive" assumption.


* 
**The Assumption:** It assumes that every single predictor is strictly independent of all other predictors.


* 
**Joint Probability Calculation:** Because variables are assumed independent, the joint probability is calculated simply by multiplying the individual probabilities together.


* 
**Continuous Data:** For continuous predictors, the model typically assumes a normal distribution or uses kernel density estimation to estimate probabilities.


* 
**Discrete Data:** For qualitative predictors, probabilities are estimated by calculating the proportion of counts in the training data.


* **Final Output:** It uses Bayes' Theorem by multiplying the prior probability by the product of the independent density functions, resulting in a conditional probability model.

---

### Poisson Regression

* 
**Use Case:** Applied exclusively when the response variable ($y$) is a non-negative integer "count", such as the number of bike riders.


* 
**Linear Model Failure:** Linear regression is inappropriate for count data because it outputs continuous real numbers and can predict physically impossible negative values.


* 
**Distribution Assumption:** The response variable is modeled following a Poisson distribution.


* 
**Expectation:** The expected value of the response variable is denoted as $\lambda$, which has a domain from zero to positive infinity.


* 
**Log Transformation (Link):** To match the mathematical domain of the linear predictors (negative to positive infinity) with $\lambda$ (zero to positive infinity), a log transformation is taken on both sides.


* **The Model:** The final expectation is modeled as $\lambda = e^{\beta_0 + \beta_1x_1 + \dots + \beta_px_p}$.


* 
**Optimization:** The coefficients ($\beta$) are estimated by maximizing the log-likelihood function using numerical methods like Newton-Raphson.


* **Interpretation:** A one-unit increase in a predictor $x_j$ multiplies the expected count by $e^{\beta_j}$.

---

### Generalized Linear Models (GLM)

* 
**Unified Framework:** GLM provides a single mathematical umbrella that unifies linear regression, logistic regression, and Poisson regression.


* 
**Link Function:** It introduces a "link function" to connect the linear combination of predictors to the expected value of the response.


* 
**Specific Links:** Linear regression uses an identity link ($\mu$), logistic uses a logit link ($\log(\frac{\pi}{1-\pi})$), and Poisson uses a log link ($\log(\lambda)$).


* 
**Exponential Family:** GLM accommodates any response variable that follows a distribution from the Exponential Family, which includes Gaussian, Bernoulli, Poisson, Exponential, Gamma, and Negative Binomial distributions.


* **Implementation:** In Python's `statsmodels` module, these diverse models are all estimated using the unified `GLM` function.

---

### K-Nearest Neighbors (KNN)

* 
**Use Case:** A non-parametric classification method used when the underlying probability distribution of the dataset is completely unknown.


* 
**Distance Metric:** It relies on calculating the Euclidean distance between a new observation and every single point in the training dataset.


* 
**Classification Rule:** It identifies the $k$ closest neighbors and assigns the new observation to the majority class among those neighbors.


* 
**Scale Sensitivity:** KNN performance is highly sensitive to the scale of the predictors; variables with larger magnitudes will unfairly dominate the distance calculation.


* **Standardization:** It is absolutely mandatory to standardize every predictor (subtract the mean, divide by standard deviation) before applying the Euclidean distance formula.



# 2/25 Lecture

### Exam Logistics & Preparation

* The midterm exam is scheduled for next Wednesday, and a step-by-step problem-solving review session will happen next Monday. 


* The exam is entirely paper-based, meaning laptops, iPads, cell phones, and internet access are strictly prohibited. 


* You are only permitted to use a calculator, pen, or pencil. 


* The test is open-book, allowing you to bring printed materials such as notes, old slides, or handwritten cheat sheets. 


* You are responsible for bringing your own formula sheets, as technical questions about forgotten formulas will not be answered during the test. 


* There are absolutely no makeup or retake exams offered; missing the exam results in an automatic zero. 

---

### Python & Data Preparation Basics

* Instead of building complex algorithms from scratch, utilize existing modules like `statsmodels`, `pandas` (often aliased as `pd`), and `numpy`. 


* Use `pd.read_csv()` to load spreadsheet data into a Pandas DataFrame. 


* A DataFrame differs from a standard matrix because it includes specific row indices and column title blocks. 


* You can check the structure of your objects using built-in functions like `type()`, `.shape`, or `.corr()` to view correlation matrices. 


* To select specific data blocks, use the `.iloc[]` function with row and column index ranges (e.g., isolating rows 5 through 7 and columns 2 through 5). 


* When preparing your predictor matrix ($X$), you must manually add a column of ones to account for the intercept, which can be done using numpy's `np.ones()` matched to the dataset's row count. 

---

### Linear & Multiple Regression Evaluation (Homework 2)

* Use `sm.OLS(y, x).fit()` from the `statsmodels` package to estimate your regression model. 


* The `.summary()` function outputs critical metrics, including the F-statistic, p-values, R-squared, coefficients, standard errors, t-statistics, and confidence intervals. 


* Alternatively, coefficients can be calculated manually using the matrix algebra formula $\beta = (X^T X)^{-1} X^T y$ by utilizing numpy functions like `np.transpose()`, `np.linalg.inv()`, and `np.dot()` or the `@` symbol. 


* 
**T-statistic:** Calculated by taking the estimated coefficient divided by its standard error. 


* The null hypothesis for a t-test assumes the coefficient equals zero ($\beta_j = 0$), meaning no relationship exists between the predictor and response. 


* 
**R-squared ($R^2$):** Represents the percentage of variance explained by the model, calculated as $SSR/SST$ or $1 - (SSE/SST)$. 


* 
**ANOVA Relationships:** Total Sum of Squares ($SST$) equals Regression Sum of Squares ($SSR$) plus Error Sum of Squares ($SSE$). 


* Mean Square Error ($MSE$) is calculated as $SSE$ divided by its degrees of freedom ($n-p$), and it represents the estimated variance of your residuals ($\sigma^2$). 


* **Extra Sum of Squares Method:** Used to test if adding new predictors or interaction terms significantly improves the model. 


* To run this test, calculate the difference in $SSR$ between the full model and the reduced sub-model, divide by the number of added predictors, and divide that entire result by the $MSE$ of the full model. 


* **Mallows' $C_p$:** A metric to evaluate reduced models, calculated using the $SSE$ of the reduced model, the $\sigma^2$ of the full model, the sample size, and the number of predictors. 


* You should select the reduced model where the $C_p$ value is closest to the number of predictors ($p$). 


* **Collinearity:** When two predictors are strongly correlated, one may appear statistically insignificant (high p-value) and should be removed from the model. 

---

### Classification & Advanced Models (Homework 3)

* 
**Quadratic Discriminant Analysis (QDA):** Unlike linear models, QDA assumes that the variance/covariance ($\Sigma_k$) is different for every single class, leading to a non-linear, quadratic decision boundary. 


* **Logistic Regression Data Formats:** 


  * *Bernoulli format:* Every individual row represents one outcome (e.g., one person survived or died). 


  * *Binomial format:* Data is grouped or aggregated (e.g., by age ranges), requiring the response variable ($y$) to include two columns representing successes and failures. 

* 
**Multinomial Logistic Regression:** Used when the response variable has more than two classes (e.g., three different high school programs), applying functions like `MNLogit`. 


* When building models in Python, if a predictor is purely categorical (like race or school type), you must wrap the variable name in `C()` within your formula so the module handles it correctly. 


* 
**Poisson Regression:** Applied when the response variable is a count of events represented by non-negative integers (e.g., the number of awards earned). 


* To estimate a Poisson model, use the `sm.GLM` function and specify the Poisson family. 



# 3/2 Lecture

### Exam Logistics & Policies

* 
**Format**: The midterm is a paper-based, open-book, and open-notes exam.


* 
**Allowed Materials**: You may bring your own prepared cheat sheet, printed lecture slides, or textbook. A standard calculator capable of computing exponential functions is required.


* **Prohibited Items**: Laptops, iPads, internet access, and other electronic communication devices are strictly forbidden. There is no Python coding required on the exam.


* **Attendance Policy**: There are no make-up or retake exams available due to resource and time constraints. Missing the exam for any reason will result in a zero.

---

### 1. Linear Regression & Matrix Formulation

* 
**Input Matrix ($X$)**: The first column of the input matrix $X$ is filled with ones to estimate the intercept $\beta_0$, and subsequent columns contain values for predictors $X_1$ to $X_p$.


* 
**Model Size ($p$)**: If you have $k$ predictors, the size of the model $p = k + 1$ (accounting for the intercept). A covariance matrix that is $3 \times 3$ indicates $k = 2$ predictors.


* 
**Coefficient Estimation**: The formula to estimate the regression coefficients is $\hat{\beta} = (X^T X)^{-1} X^T Y$.


* 
**Covariance & Variance**: The covariance matrix for the $\beta$ coefficients is $\sigma^2 C$, where $C = (X^T X)^{-1}$.


* **Standard Error**: The variance of a specific coefficient $\hat{\beta}_j$ is calculated as $\sigma^2 C_{jj}$. The standard error is the square root of its variance.

---

### 2. ANOVA, $R^2$, and Hypothesis Testing

* **Sum of Squares**:

  * **$SST$ (Total Sum of Squares)**: Measures total variation in $Y$ ($SST = \sum (y_i - \bar{y})^2$). $SST$ remains unchanged even if you add new predictors to the model.


  * **$SSR$ (Regression Sum of Squares)**: Represents the amount of variation explained by your model.


  * **$SSE$ (Error Sum of Squares)**: Represents the unexplained variation, calculated as $SST - SSR$.



* **$R^2$ and Adjusted $R^2$**:


  * 
    $R^2 = \frac{SSR}{SST}$.


  * Adjusted $R^2$ accounts for degrees of freedom: $1 - \frac{SSE / (n-p)}{SST / (n-1)}$.



* **Overall Significance (F-Test)**:


  * Tests the null hypothesis ($H_0$) that all coefficients $\beta_1 = \beta_2 = ... = 0$ against the alternative that at least one $\beta_j \neq 0$.


  * 
  $F = \frac{MSR}{MSE} = \frac{SSR / k}{SSE / (n-p)}$.


  * Degrees of freedom: Numerator $df_1 = k$, Denominator $df_2 = n - p$.


  * If the calculated F-statistic is greater than the critical value from the F-distribution table, you reject $H_0$ and conclude the model is statistically significant.


  * **Partial F-Test (Adding Predictors)**:


  * Evaluates if adding new regressors significantly improves the model.


  * 
  $F = \frac{(SSR_{full} - SSR_{reduced}) / r}{MSE_{full}}$, where $r$ is the number of new predictors added.


  * Degrees of freedom: Numerator $df_1 = r$, Denominator $df_2 = n - p_{full}$.


  * If $F < F_{critical}$, you fail to reject $H_0$, meaning the coefficients of the added predictors are statistically zero and any apparent benefit is due to randomness.



* **Mallows' $C_p$**: Used to compare sub-models. You evaluate which model's $C_p$ value is closest to $p$ (the number of parameters).

---

### 3. Model Flexibility: LDA vs. QDA & Polynomial Regression

* **Linear True Decision Boundary**:

  * **Training Error**: Flexible models like QDA or Cubic Regression will always have a lower training error (smaller SSE) because they fit the training data more closely.


  * **Test Error**: Simpler models like LDA or Simple Linear Regression will perform better on unseen test data, as flexible models will overfit the true linear relationship.



* **Non-Linear True Decision Boundary**:


  * **Training Error**: Flexible models (QDA, Cubic) again perform better.


  * **Test Error**: Generally, flexible models perform better for prediction. However, if the true relationship is non-linear but very close to linear, a linear model might still=yield better predictions.



* **Sample Size Impact**: As the sample size ($n$) increases, the prediction accuracy of more flexible methods (like QDA) improves relative to simpler methods.

---

### 4. Logistic Regression

* 
**Distribution**: Logistic regression is used when the response variable $Y$ has binary outcomes (e.g., 1 for success, 0 for failure) and follows a Bernoulli distribution.


* **Probability Equations**:


  * 
    $P(Y=1|X) = \frac{e^{\beta_0 + \beta_1 X_1 + \beta_2 X_2}}{1 + e^{\beta_0 + \beta_1 X_1 + \beta_2 X_2}}$.


  * 
  $P(Y=0|X) = \frac{1}{1 + e^{\beta_0 + \beta_1 X_1 + \beta_2 X_2}}$.



* 
**Solving for Predictors**: To find the value of a predictor needed to achieve a specific probability, use the log-odds format: $\ln(\frac{p}{1-p}) = \beta_0 + \beta_1 X_1 + \beta_2 X_2$.


* **Variable Coding**: Coding a binary response variable as $\{0, 1\}$ versus $\{-1, 1\}$ alters the mathematical form of the model equations and mass functions, but it remains consistent and will yield the exact same probabilities given the same inputs.

---

### 5. Bayes Classifiers

* **Model Assumptions**:

  * **LDA**: Assumes all classes share a common variance ($\sigma^2$).


  * **QDA**: Assumes variances differ between classes.



* 
  **Bayes Theorem**: To calculate the conditional probability $P(Y=k|X)$, use the formula: $\frac{\pi_k f_k(x)}{\sum \pi_l f_l(x)}$.


  * 
  $\pi_k$ is the prior probability of class $k$ (e.g., the proportion of the population belonging to that class).


  * $f_k(x)$ is the density function for class $k$. If assuming a normal distribution, $f(x) = \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x-\mu_k)^2}{2\sigma^2}}$.



* **Naive Bayes**: Used when there are multiple predictors. It assumes that predictors $X_1, X_2, \dots$ are completely independent, meaning you can calculate the joint probability by simply multiplying the individual marginal probabilities (likelihoods) together.
