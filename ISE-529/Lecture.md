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

    $$Z = \frac{X - \mu}{\sigma}$$

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

Here is a detailed "cheatsheet" style lecture note based on the provided transcript.

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
   - *Flaw:* A low training MSE does not guarantee a good model; it typically decreases monotonically as flexibility increases.
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