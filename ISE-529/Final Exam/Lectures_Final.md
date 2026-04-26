# 3/9 Lecture

## Tree-Based Methods: High-Level Overview

Tree-based methods stratify or segment a predictor space into distinct sub-areas (regions). They are highly versatile and can be applied to both numerical and categorical data.

* **Regression Trees:** Used when the response variable is numerical (e.g., predicting stock prices or baseball salaries).
* **Classification Trees:** Used when the response variable is categorical (e.g., predicting "Yes" or "No" for playing golf based on the weather). 
* **The "Tree" Structure:** The final model visually resembles an upside-down tree. The starting point is at the top, and the final predictions are at the bottom.
* **Prediction Output:** The model uses the mean (for regression) or the mode/majority vote (for classification) of the response variables within each segmented sub-area as the final prediction.
* **Collinearity Immunity:** Unlike linear regression, tree methods do not suffer from collinearity. You do not need to drop highly correlated predictors.

### Limitations & Advanced Tree Algorithms
A single decision tree has limited possible outputs and generally cannot compete with the predictive accuracy of a linear regression model for continuous data. 

To improve overall performance, flexibility, and accuracy, data scientists use advanced algorithms that build thousands of trees and aggregate their outputs. These include:
* **Bagging**
* **Random Forests**
* **Boosting**

---

## Tree Terminology

| Term | Definition |
| :--- | :--- |
| **Root Node** | The very top node of the tree. It represents the most significant, important predictor in the entire dataset. |
| **Decision Node** | Internal nodes where the data is split based on a specific predictor's condition. |
| **Branches** | The lines connecting nodes, representing the specific conditions or categories of a split. |
| **Leaf Node (Terminal Node)** | The final endpoints at the bottom of the tree representing the model's ultimate prediction or classification. |
| **Predictor Space** | The multi-dimensional space created by all input variables. Trees work by vertically slicing this space into smaller boxes. |

---

## Building a Classification Tree

Classification trees use a **Top-Down Greedy Search Method** (originally proposed by J.R. Quinlan). It is "greedy" because it only looks for the optimal split at the current local level, without worrying about the global optimum of the future tree.

### 1. The Core Metrics: Entropy & Information Gain

To decide which predictor should be used for a split, the algorithm calculates how well a predictor groups similar response variables together (homogeneity). 

* **Entropy:** A metric used to estimate homogeneity. The value always falls between 0 and 1.
* **Complete Homogeneity (Entropy = 0):** All observations in the group belong to a single class. The branch cannot be split further.
* **Complete Heterogeneity (Entropy = 1):** The observations in the group are equally split (e.g., 50/50) between classes.
* **Entropy Formula:** For a categorical variable with probabilities $p_1$ and $p_2$, the formula is:
    $Entropy = - (p_1 \log_2(p_1) + p_2 \log_2(p_2))$
* **Information Gain:** The measurable benefit of splitting the data using a specific predictor. It is the difference between the total entropy before the split and the weighted entropy after the split. 

### 2. Step-by-Step Construction Process

1.  **Calculate Total Entropy:** Look at your target variable (e.g., "Play Golf: Yes/No") and calculate its total entropy using the proportions of Yes vs. No.
2.  **Build Frequency Tables:** For every single predictor, create a cross-tabulation comparing its categories against the target variable.
3.  **Calculate Weighted Entropy:** For each predictor, calculate the entropy of each of its branches, then calculate the weighted average of those entropies based on the number of observations in each branch.
4.  **Calculate Information Gain:** Subtract the predictor's weighted entropy from the total target entropy.
5.  **Select the Node:** The predictor yielding the **highest Information Gain** becomes the decision node (or root node if it's step one).
6.  **Reorganize & Repeat:** Split the dataset into subsets corresponding to the branches of the chosen node. Repeat steps 1-5 for each new subset.
7.  **Stop:** Stop growing a branch when a subset reaches an Entropy of 0 (a pure Leaf Node).

---

## Building a Regression Tree

When the target variable is continuous, the concept remains similar, but the math and splitting criteria change.

### 1. The Core Metric: Residual Sum of Squares (RSS)

Instead of Information Gain, regression trees aim to minimize the total variation or error within the created sub-regions. The algorithm seeks the split that groups the most numerically similar target values together.

* **Objective Function:** The goal is to minimize the total variation using the following function:
    $\sum_{j=1}^{J} \sum_{i \in R_j} (y_i - \hat{y}_{R_j})^2$
* $R_j$: The specific distinct, non-overlapping sub-region.
* $y_i$: The actual observed target value.
* $\hat{y}_{R_j}$: The mean target value of all observations falling inside region $R_j$.

### 2. Recursive Binary Splitting

Because continuous predictors can take on an infinite number of real values, the algorithm cannot feasibly test every single number as a splitting point.

* **Binary Cuts Only:** To keep computations feasible, the algorithm only splits a predictor space into two branches at a time (e.g., $X < 4.5$ and $X \ge 4.5$).
* **Candidate Testing:** The algorithm selects a limited number of candidate cutting points evenly distributed between the predictor's lower and upper bounds (e.g., 10 candidate points).
* **Evaluation:** It tests each of these candidate points by calculating the Objective Function (total variation) for the two resulting groups. 
* **Selection:** The cutting point that yields the absolute minimum total variation is selected as the optimal split.

### 3. Stopping Criteria

Since continuous data rarely reaches perfect zero-variation purity, you must define rules to tell the algorithm when to stop cutting to prevent over-splitting.

* **Observation Threshold:** A common stopping criterion is dictating that the algorithm must stop splitting if a resulting region contains fewer than a specific number of observations (e.g., stop if a leaf node would contain fewer than 5 observations).



# 3/11 Lecture

## 1. Regression Trees (Quantitative Response Variables)

Used when the response variable takes continuous, real values (e.g., salary, price).

- **Recursive Binary Splitting:** The algorithm finds a single cutting point for one predictor at a time, splitting the predictor space into two branches (left and right).

  - *Why Binary?* Splitting into multiple pieces at once is computationally infeasible.

- **The Objective Function:** The goal is to minimize the total variation (sum of squared differences) within the newly created subgroups.

  $$Total\ Variation = \sum_{i=1}^{N} (y_i - \bar{y})^2$$

  - The algorithm tries all candidate cutting points and chooses the one that produces the minimum value from this objective function (maximizing homogeneity).

- **Making a Prediction:** Once the tree is built, the final "leaf nodes" (terminal nodes) represent small subgroups of the data. The model's predicted value for any new observation falling into a specific leaf node is the **sample mean** of the training observations in that node.

------

## 2. Tree Pruning & Cross-Validation

A fully grown decision tree (where every leaf node might only contain 1 observation) will perfectly fit the training data but will fail to generalize to new data. This is known as **overfitting**.

- **Why Greedy Search Fails:** Simply setting a threshold (e.g., "only split if the reduction in error is > 100") doesn't work. A split that yields a small improvement *now* might lead to a massive improvement further down the tree. Local optimal $\neq$ Global optimal.

- **Cost Complexity Pruning:** The solution is to grow a massive, full-size tree first, and then "prune" it backward by chopping off branches to see if it improves the test error.

- **Pruning Objective Function:** You evaluate subtrees using a penalized objective function:

  $$Error + \alpha |T|$$

  - $|T|$ = The model size (total number of leaf nodes).
  - $\alpha$ = A tuning/control parameter.
  - If $\alpha = 0$, you get the full tree. As $\alpha$ increases, the penalty for having a large tree increases, forcing the model to favor smaller, simpler trees.

- **K-Fold Cross-Validation:** Used to find the optimal $\alpha$.

  1. Divide the dataset into **K** equal portions (folds).
  2. Hold out one portion as the test set, and train the model on the remaining $K-1$ portions.
  3. Calculate the Mean Squared Error (MSE) on the holdout test set.
  4. Repeat this $K$ times, holding out a different portion each time.
  5. Average the MSEs. Pick the $\alpha$ (and the corresponding subtree size) that produces the lowest average prediction error.

------

## 3. Classification Trees (Categorical Response Variables)

Used when the response variable falls into a finite set of classes (e.g., "Yes/No", "Healthy/Heart Disease").

- **Making a Prediction (Majority Vote):** Instead of calculating the mean, a leaf node predicts the class that occurs most frequently among the training observations in that node.

- **Level of Confidence:** The model doesn't just output the class; it outputs the proportion. For example, if a leaf node has 10 observations (7 "Yes", 3 "No"), the prediction is "Yes" with a 70% level of confidence.

- **Splitting Criteria (Evaluating Homogeneity/Purity):**

  - *Classification Error Rate:* **Do not use this** for building the tree. It is not sensitive enough to node purity.

  - **Gini Index:** The standard metric used to evaluate splits. It measures node purity.

    $$Gini = \sum_{k=1}^{K} p_{mk} (1 - p_{mk})$$

    - $p_{mk}$ is the proportion of training observations in the $m$-th region that belong to the $k$-th class.
    - If a node is perfectly pure (all observations belong to one class), the Gini index approaches **0**.

  - **Entropy:** An alternative to the Gini index that works very similarly, utilizing $\log_2$. Like Gini, a smaller entropy value indicates a purer node.

------

## 4. Pros and Cons of Decision Trees

**Advantages:**

- **Highly Interpretable:** Easy to explain to non-experts (like medical doctors). Graphic representations mirror human decision-making.
- **No Dummy Variables Needed:** Easily handles categorical (qualitative) predictors natively.
- **Immune to Collinearity:** You don't need to worry about strong correlations between pairs of predictors; the tree will naturally handle them without skewing the model.

**Disadvantages:**

- **Lower Predictive Accuracy:** Compared to linear regression, standard decision trees have lower accuracy. A tree can only output a finite number of predictions (equal to the number of leaf nodes), whereas linear regression has infinite possible outputs.
- **High Variance:** Small changes in the training data can result in a vastly different tree structure.

------

## 5. Ensemble Methods: Mitigating High Variance

Because single decision trees are "weak learners" (unstable and high variance), we use ensemble methods to combine many trees together to create a highly accurate, robust model.

- **The Theoretical Math:** If you have $n$ independent observations with variance $\sigma^2$, the variance of their mean is significantly smaller:

  $$Var(\bar{X}) = \frac{\sigma^2}{n}$$

  - *Translation:* Averaging a set of random variables drastically reduces the overall variance.

- **Bagging (Bootstrap Aggregating):**

  - Build hundreds or thousands of separate decision trees.
  - Pass the same input into every single tree.
  - Average the outputs of all the trees to get your final, highly stable prediction.
  - *Note on Data:* Since you only have one dataset, you use a technique called **Bootstrapping** (to be covered in the next lecture) to duplicate and sample your data so you can build all these different trees.



# 3/23 Lecture

------

### **Admin Notes: Midterm & Final**

- **Midterm Curve:** Scores were adjusted with an average curve of +20 points (e.g., original 50s became 70s, 60s became 80s).
- **Expectations:** The exam questions were drawn directly from lecture material. Attendance and reviewing the provided videos are highly recommended for the final exam.

------

### **1. The Problem with Single Decision Trees**

While single decision trees are easy to interpret and visualize, they are generally not competitive with other methods (like linear regression) regarding prediction accuracy.

- **High Variance:** Single decision trees suffer from high variance. If you split a dataset in half and train a decision tree on each half, you will get two vastly different trees. The model is too sensitive to minor changes in the training data.

### **2. Ensemble Methods: The Solution**

**Core Idea:** Combine multiple "weak" single models to create a single, powerful aggregated model.

- **Theoretical Basis:** Averaging independent variables reduces variance. If every variable $x$ has a variance of $\sigma^2$, the variance of the sample mean $\bar{x}$ is significantly smaller:

  $$Var(\bar{X}) = \frac{\sigma^2}{n}$$

- By generating $B$ different trees and averaging their outputs (or taking a majority vote), we significantly reduce the overall model variance.

------

### **3. Bagging (Bootstrap Aggregation)**

Bagging applies the ensemble theory to decision trees using a resampling technique called Bootstrapping.

**The Bootstrapping Technique:**

Since we cannot infinitely collect new data, we simulate new datasets from our original dataset of size $n$.

- We randomly draw an observation from the original dataset, copy it to the new dataset, and return it to the original pool (sampling with replacement).
- Repeat this $n$ times to create a new "Bootstrapped" dataset of the same size.
- Repeat this process to create $B$ different datasets, then train $B$ different decision trees.

**Key Characteristics of Bagging:**

- **Deep Trees:** The individual trees are grown deep and are not pruned. This means each tree has *high variance* but *low bias*.
- **Aggregation:** * *Regression:* Average the numerical outputs of all $B$ trees.
  - *Classification:* Take a "majority vote" among all $B$ trees.
- **Out-of-Bag (OOB) Observations:** Because bootstrapping uses sampling with replacement, some original observations are left out of each new dataset.
  - Probability of a single observation *not* being chosen: $1 - \frac{1}{n}$
  - Probability of it not being chosen after $n$ draws: $(1 - \frac{1}{n})^n$
  - As $n$ becomes large, $(1 - \frac{1}{n})^n \approx e^{-1} \approx 0.36$.
  - Therefore, roughly $\frac{1}{3}$ of the data is left out of any given bootstrapped dataset. This "Out-of-Bag" data can be used directly as test data to calculate errors (like MSE) without needing a separate validation set.
- **Side Benefit:** Bagging allows us to calculate feature importance by tracking which predictors yield the highest total Information Gain or Gini index reduction across all trees.

------

### **4. Random Forests**

Random Forests are an improvement over Bagging designed to fix the problem of **tree correlation**.

- **The Flaw in Bagging:** If there is one extremely strong predictor in the dataset, almost every bootstrapped tree will use that same predictor for its top split (root node). As a result, all $B$ trees look similar and their predictions are highly correlated. Averaging highly correlated trees does *not* reduce variance effectively.
- **The Random Forest Solution:** Every time the algorithm considers a split, it is *only* allowed to choose from a random subset of $m$ predictors, rather than all $p$ predictors.
- **Rule of Thumb for $m$:** Typically, $m = \sqrt{p}$.
  - *Note:* If $m = p$, the Random Forest algorithm acts exactly like standard Bagging.
- By restricting the candidate predictors, the algorithm is forced to build structurally different, uncorrelated trees, leading to a much stronger ensemble when averaged.

------

### **5. Boosting**

Boosting takes a completely different approach from Bagging/Random Forests. Instead of building independent trees in parallel, trees are grown **sequentially**, with each tree learning from the mistakes of the previous one.

**Key Characteristics:**

- No bootstrapping is used; it operates on the original dataset.
- Trees are usually very small (e.g., $d=1$, a "stump" with a single split).

**The Boosting Algorithm Steps (Regression Example):**

1. **Initialize:** Set the initial model output to 0. Set the residuals $r_i$ equal to the original response variable $y_i$.
2. **Iterate ($B$ times):**
   - **Fit:** Fit a small decision tree using the inputs $X$ to predict the *current residuals* $r_i$ (not the original $y_i$).
   - **Update Model:** Add this new tree's output to the total model output, scaled by a learning rate/shrinkage parameter ($\lambda$).
   - **Update Residuals:** Subtract the scaled predictions of the new tree from the current residuals: $r_i = r_i - \lambda \hat{f}(x)$.
3. **Result:** The final model is the accumulated sum of all sequential trees.

**Tuning Parameters in Boosting:**

- **$B$ (Number of trees):** Unlike Bagging, a very high $B$ in Boosting *can* lead to overfitting because it will eventually just learn the noise in the residuals. Use Cross-Validation to find the optimal $B$.
- **$\lambda$ (Shrinkage parameter):** Controls the learning rate (typically 0.01 or 0.001). A smaller $\lambda$ requires a larger $B$.
- **$d$ (Splits/Depth):** Controls the complexity of each tree. Often, $d=1$ (stumps) yields the best results.

------

### **6. Python Implementation (`scikit-learn`)**

**Libraries Used:**

- `sklearn` (specifically `DecisionTreeClassifier`, `DecisionTreeRegressor`, `RandomForestClassifier`, etc.)
- `pandas` & `numpy` (data manipulation)
- `matplotlib` (plotting results and visualizing trees)

**Core Syntax Workflow:**

1. **Initialize the Model:** e.g., `clf = DecisionTreeClassifier(criterion='gini', max_depth=5, random_state=0)`
2. **Fit the Model:** `clf.fit(X_train, y_train)` (This executes the algorithm/math behind the scenes).
3. **Make Predictions:** `clf.predict(X_test)`
4. **Visualize:** You can plot the resulting tree.
   - *Interpreting Leaf Nodes:* A printed tree node will show the Gini/Entropy score, the total number of samples falling into that node, and the class breakdown.
   - For classification, the model predicts the majority class in that leaf.
   - For regression, the model predicts the average (mean) value of the samples in that leaf.

**Trade-off Note:** While Ensemble methods (Bagging, Random Forests, Boosting) drastically improve accuracy over a single decision tree, you lose the simple visual interpretability of looking at a single flow chart to explain the model's exact decision path.



# 3/25 Lecture

## Resampling Methods: Cross-Validation & Bootstrap

Resampling methods involve repeatedly drawing samples from a training dataset and refitting a model of interest on each sample. These techniques allow us to obtain additional information about the fitted model, without the cost of collecting new data.

### Core Purposes of Resampling

- **Model Assessment:** Evaluating how well a model's predictions perform on unseen data (estimating test error).
- **Model Selection:** Choosing the best model flexibility level or the best algorithm among a set of candidates.

------

## 1. Validation Set Approach

This is the simplest way to estimate test error by splitting the original data into two subsets.

- **Method:** Arbitrarily split the original dataset into a Training Set and a Validation (Holdout) Set.
- **Process:** Train the model on the Training Set, then make predictions on the Validation Set to calculate the Test Mean Squared Error (MSE).
- **Issues:** The estimate of the test error is highly variable depending on exactly which observations end up in which set.
- **Issues:** Because it uses only a subset of the data to train, it tends to overestimate the true test error of a model fit on the entire dataset.

------

## 2. Leave-One-Out Cross-Validation (LOOCV)

LOOCV attempts to address the drawbacks of the Validation Set approach by maximizing the training data used.

- **Method:** From $n$ observations, use $n-1$ observations to train the model, leaving exactly 1 observation out as the validation set.
- **Process:** Repeat this process $n$ times, leaving a different observation out each time.
- **Calculation:** Calculate the test MSE for each single held-out observation, then average all $n$ MSEs to find the final predicted test error.
- **Advantages:** Far less bias because it trains on nearly the entire dataset. It yields consistent results with no randomness depending on data splitting.
- **Disadvantages:** Extremely computationally expensive, especially for large datasets or complex models (e.g., running a Neural Network $10,000$ times).
- **Linear Regression Shortcut:** For Least Squares Linear Regression, LOOCV can be computed in a single step without repeating the fit $n$ times using the Hat Matrix ($H$). The calculation uses $h_i$, the elements along the major diagonal of the Hat Matrix, representing the variance of the predicted values.

------

## 3. k-Fold Cross-Validation

This method strikes a balance between computational efficiency and statistical accuracy.

- **Method:** Randomly divide the dataset into $k$ equal-sized groups (folds).
- **Process:** Leave 1 fold out as the validation set, and train the model on the remaining $k-1$ folds. Repeat this $k$ times, with each fold acting as the validation set exactly once.
- **Calculation:** Average the $k$ resulting MSE values to estimate the test error.
- **Typical Values:** In practice, $k=5$ or $k=10$ are standard as they are computationally feasible and offer good empirical performance.
- **Equivalence:** LOOCV is a special case of k-Fold Cross-Validation where $k=n$.

------

## 4. Bias-Variance Tradeoff: LOOCV vs. k-Fold

| **Feature**          | **LOOCV**                                                    | **k-Fold (k=5 or 10)**                                       |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Bias**             | **Low:** Models are trained on almost the entire dataset ($n-1$). | **Intermediate:** Models are trained on a slightly smaller portion of the data. |
| **Variance**         | **High:** The $n$ trained models use nearly identical datasets, meaning their predictions are highly correlated. The average of highly correlated variables does not reduce variance much. | **Lower:** The $k$ trained models have less overlap in their training data, making them less correlated. Averaging less correlated variables effectively reduces variance. |
| **Computation Time** | **High:** Requires fitting the model $n$ times.              | **Low:** Requires fitting the model only $k$ times.          |

------

## 5. Evaluating Classification Models

When dealing with categorical (classification) responses rather than quantitative (regression) responses, the evaluation metric shifts.

- **Metric:** Instead of Test MSE, use the Misclassification Error Rate.
- **Indicator Function ($I$):** This function compares the model's predicted class to the observed class. It outputs 1 if they do not match (misclassified) and 0 if they match.
- **Calculation:** Sum the outputs of the Indicator Function to get the total number of misclassified observations, then divide by the total number of observations ($n$) to find the error rate.

------

## 6. The Bootstrap Technique

Bootstrap allows for the quantification of uncertainty associated with a given estimator or machine learning method (e.g., calculating standard errors or confidence intervals).

- **Method:** Repeatedly draw random samples from the original dataset **with replacement** to create new datasets.
- **Size Constraint:** Every new bootstrap dataset must contain the exact same number of observations ($n$) as the original dataset.
- **Out-of-Bag (OOB) Observations:** Because sampling is done with replacement, some original observations will be duplicated in the new dataset, while roughly one-third of the original observations will be entirely left out of any given bootstrap sample.
- **Use Cases:** Essential for ensemble algorithms like Bagging and Random Forests (e.g., building multiple decision trees).

### Bootstrap Application Example: Risk Minimization in Investments

- **Scenario:** Splitting an investment between two stocks ($X$ and $Y$) by allocating fraction $\alpha$ to $X$ and $1-\alpha$ to $Y$.
- **Goal:** Minimize the risk (variance) of the total return.
- **Mathematical Objective:** Minimize $\text{Var}(\alpha X + (1-\alpha)Y)$.
- **Formula Expansion:** $\alpha^2 \sigma_X^2 + (1-\alpha)^2 \sigma_Y^2 + 2\alpha(1-\alpha)\sigma_{XY}$
- **Solution:** By taking the first-order derivative with respect to $\alpha$ and setting it to zero, an exact formula for the optimal $\alpha$ is derived.
- **Bootstrap Validation:** When testing this theoretically derived $\alpha$ (which is roughly 0.6) against 1,000 generated datasets, the Bootstrap method provides an average $\alpha$ nearly identical to a complex Monte Carlo simulation, proving Bootstrap's reliability.

------

## 7. Python Implementation

Resampling techniques are standardized and easily implemented using Python's `scikit-learn` package.

- **Library:** Import functions from the `sklearn.model_selection` module.
- **k-Fold CV:** Use the `KFold` function to define the splits (e.g., `n_splits=5` or `10`, with optional random shuffling).
- **Execution:** Pass the model, data, and CV strategy into the `cross_validate` function to automatically execute the iterations and return the error metrics.



# 3/30 Lecture

## 1. The Problem: High Dimensionality

In modern data analysis (e.g., gene expression), datasets often contain massive numbers of predictors (e.g., 4,718 columns with only 349 observations).

- **The Limit:** Traditional linear regression models cap out at roughly 200 predictors.
- **The Solution:** **Dimension Reduction**. Shrink a high-dimensional original matrix ($X$) into a smaller matrix ($Y$) while retaining the "geometry" or dynamic information (total variation/variance) of the original data.

------

## 2. Mathematical Prerequisites

Before diving into PCA, several algebraic concepts are required.

### Eigenvalues & Eigenvectors

For a square matrix $\Sigma$, if we can find a vector $\gamma$ and a scalar $\lambda$ such that:

$$\Sigma \gamma = \lambda \gamma$$

- **$\gamma$** is the **Eigenvector**.
- **$\lambda$** is the **Eigenvalue**.
- **How to solve:** Rewrite as $\gamma(\Sigma - \lambda I) = 0$ (where $I$ is the Identity Matrix). Set the determinant to zero ($|\Sigma - \lambda I| = 0$) and solve for $\lambda$, then plug it back in to find $\gamma$.

### Orthogonal & Orthonormal Vectors

- **L2 Norm (Length of a vector):** $\sqrt{\sum x_i^2}$. A unit vector has an L2 norm of 1.
- **Orthogonal:** Two vectors are perpendicular in hyper-space. Their dot product (inner product) is zero.
- **Orthonormal:** Two vectors are orthogonal *and* they both have a unit length of 1.

------

## 3. The PCA Process (Two Steps)

PCA is split into two distinct steps: Mathematical Transformation and Dimension Reduction.

### Step 1: Transformation (High Dimension to High Dimension)

Convert the original $N \times D$ dataset into a new $N \times D$ dataset.

- **Original Data ($X$):** Columns are highly correlated.
- **Transformed Data ($Y$):** Columns are strictly **uncorrelated** (resolving multicollinearity).
- **Variance Sorting:** The transformed columns (variables) are ordered in descending order of variance. The first column captures the largest proportion of the total sample variance, the second column captures the second largest, and so on ($\lambda_1 > \lambda_2 > \lambda_3 \dots$).
- **PC Scores:** The columns in the new matrix $Y$ are called Principal Component (PC) scores. They are linear combinations of the original variables.

### Step 2: Dimension Reduction (High Dimension to Low Dimension)

Once transformed, discard the columns with the lowest variances (the right side of matrix $Y$), keeping only the first $d$ columns that explain the majority of the data's variation.

------

## 4. How to Perform the Transformation (Two Methods)

### Method A: Spectral Decomposition Theorem

Applies strictly to **square, symmetric matrices**.

1. **Center the data:** Remove the sample mean from every column in original matrix $X$.
2. **Covariance Matrix:** Calculate the covariance matrix $\Sigma = X^T X$. This results in a square, symmetric matrix.
3. **Decompose:** Decompose $\Sigma$ into three matrices: $\Sigma = P D P^T$
   - **$P$:** A matrix where every column is an eigenvector of $\Sigma$ (these are your Principal Components).
   - **$D$:** A diagonal matrix containing the eigenvalues ($\lambda$) of $\Sigma$.
4. **Transform:** Multiply original data by the eigenvectors to get the new matrix: **$Y = X P$**

### Method B: Singular Value Decomposition (SVD)

A more generalized and numerically stable method that applies to **any rectangular matrix** ($M \times N$).

1. **Decompose Original Data:** $X = U \Lambda V^T$
   - **$U$:** Matrix containing eigenvectors of $X X^T$.
   - **$V$:** Matrix containing eigenvectors of $X^T X$ (the covariance matrix).
   - **$\Lambda$:** Diagonal matrix containing **singular values** (the square root of the eigenvalues).
2. **Transform:** The new matrix can be found by calculating: **$Y = X V$** (which is mathematically equal to $U \Lambda$).

**Total Variance Check:** In both methods, the total variance of the original dataset $X$ is equal to the sum of the eigenvalues ($\sum \lambda_i$), which is also the "trace" (sum of the major diagonal) of the covariance matrix $\Sigma$. Total variation is perfectly preserved in the complete matrix $Y$.

------

## 5. Criteria for Dimension Reduction (Choosing '$d$')

How do you decide how many columns to keep from matrix $Y$?

1. **Cumulative Variance Percentage:** Calculate the proportion of variance each PC explains ($\lambda_j / \text{Total Variance}$). Keep summing these until you hit a satisfactory threshold (e.g., 70%, 90%, or 95%). Discard the rest.
2. **Average Eigenvalue:** Calculate the average of all eigenvalues. Keep any PC whose eigenvalue ($\lambda$) is strictly greater than the average.
3. **Scree Plot (Elbow Method):** Plot the eigenvalues ($\lambda$) on the y-axis against the PC index on the x-axis. Find the "elbow" or turning point where the slope drops off sharply and flattens out. Keep the components before the elbow.

------

## 6. Covariance vs. Correlation Matrix

When calculating your eigenvectors, which matrix should you start with?

- **Covariance Matrix:** Maintains the original units of your data. *Downside:* If predictors are on vastly different scales (e.g., thousands of dollars vs. a 1-10 rating), the larger magnitude variables will unjustly dominate the variance calculation.
- **Correlation Matrix:** A standardized version of the covariance matrix. *Advantage:* It is unitless (values between 0 and 1). All predictors are put on the exact same scale, giving every variable an equal weight.

------

## 7. Principal Component Regression (PCR)

Once you have your reduced matrix $Y$ (with perfectly uncorrelated columns), you can use it to build a highly stable regression model.

- **The Model:** Run an Ordinary Least Squares (OLS) regression using the PC scores (matrix $Y$) as your predictors.
- **The Coefficients:** This yields PCR coefficients ($\theta$).
- **Back-transformation:** You can convert the PCR coefficients back into the original variables' coefficients ($\beta$) by multiplying them by the eigenvector matrix: **$\beta = P \theta$**.
- **Advantage:** PCR eliminates multicollinearity issues entirely and often captures the major data trends better than a standard OLS regression on highly collinear original data. Applications extend beyond modeling into data compression (e.g., ZIP files).



# 4/1 Lecture

## 1. Core Concepts & Motivation

- **The Problem with Ordinary Least Squares (OLS):** When predictors ($p$) are highly correlated or when $p$ is nearly equal to or greater than the number of observations ($n$), OLS estimates become highly volatile. This leads to a model with **low bias but very high variance** (unstable coefficients).
  - *Extreme Case ($n \ll p$):* Example: Gene expression data with 4,500 predictors but only 349 patients. OLS cannot find a unique mathematical solution because there are more variables than equations.
- **The Solution (Shrinkage Methods):** Introduce a "penalty" to the OLS objective function. This puts constraints on the coefficients, forcing them to shrink toward zero.
- **The Trade-off:** Shrinking coefficients introduces a small amount of **bias** into the model, but significantly reduces model **variance**, leading to better overall predictions on unseen data.

------

## 2. Ridge Regression (L2 Penalty)

Ridge regression shrinks the coefficients of less important predictors close to zero, but never exactly to zero. It retains all predictors in the final model.

- **Objective Function:** Minimize the Residual Sum of Squares (RSS) plus a shrinkage penalty.

  $$\text{Minimize: } \text{RSS} + \lambda \sum_{j=1}^p \beta_j^2$$

- **Optimization/Constraint Format:** This is mathematically equivalent to minimizing RSS subject to:

  $$\sum_{j=1}^p \beta_j^2 \le t$$

  *(Where $t$ is the constraint budget, conceptually linked to $\lambda$ via a Lagrange multiplier).*

- **The Tuning Parameter ($\lambda$):** * If $\lambda = 0$: The penalty is nullified; the result is identical to OLS.

  - If $\lambda \to \infty$: The penalty is massive; all coefficients are forced toward $0$.
  - Optimal $\lambda$ is found using **Cross-Validation** (finding the lowest test Mean Squared Error (MSE) curve).

- **Mathematical Insight (SVD):** Singular Value Decomposition ($X = UDV^T$) shows that Ridge shrinks directions with the smallest eigenvalues (variance) the most. The shrinkage factor applied is $\frac{d_j^2}{d_j^2 + \lambda}$.

------

## 3. Lasso Regression (L1 Penalty)

Lasso (Least Absolute Shrinkage and Selection Operator) improves upon Ridge by forcing the coefficients of insignificant predictors to **exactly zero**. This creates a "sparse" model, which acts as built-in variable selection and makes the model much easier to interpret.

- **Objective Function:** Uses absolute values instead of squares.

  $$\text{Minimize: } \text{RSS} + \lambda \sum_{j=1}^p |\beta_j|$$

- **Optimization/Constraint Format:**

  $$\sum_{j=1}^p |\beta_j| \le t$$

### ⚠️ IMPORTANT: The Geometric Proof (Why Lasso = 0, but Ridge $\neq$ 0)

- **Ridge Constraint Region (L2):** $\beta_1^2 + \beta_2^2 \le t$ forms a **circle** (no sharp corners).
- **Lasso Constraint Region (L1):** $|\beta_1| + |\beta_2| \le t$ forms a **diamond** (sharp corners on the axes).
- **The Intersection:** The OLS RSS forms elliptical contours. We must find where the RSS ellipse first intersects the constraint region.
  - Because the **Ridge circle** has smooth edges, the ellipse rarely hits it exactly on an axis. Thus, coefficients are small but non-zero.
  - Because the **Lasso diamond** has sharp points directly on the axes, the ellipse has a high mathematical probability of intersecting it at a corner. If the intersection happens on an axis, the corresponding coefficient ($\beta$) is **exactly 0**.

------

## 4. Elastic Net (The Hybrid)

Because neither Ridge nor Lasso universally dominates (performance is strictly data-driven), Elastic Net was created to combine the best of both.

- **Objective Function:** Combines L1 and L2 penalties using a mixing parameter $\alpha$.

  $$\text{Minimize: } \text{RSS} + \lambda \left( \alpha \sum_{j=1}^p |\beta_j| + (1-\alpha) \sum_{j=1}^p \beta_j^2 \right)$$

- **Tuning:** * If $\alpha = 1$, it becomes pure Lasso.

  - If $\alpha = 0$, it becomes pure Ridge.
  - Cross-validation is used to select both the best $\lambda$ and the best $\alpha$.

------

## 5. Pre-Processing Rules (Crucial for all Shrinkage Methods)

1. **Do NOT penalize the Intercept ($\beta_0$):** The penalty index starts at $j=1$. Penalizing the intercept would mean your model's accuracy depends on the arbitrary origin of $Y$.
2. **Standardize your Data:** Because penalties are based on the magnitude of coefficients, all predictors must be on the same scale before running Ridge/Lasso.
   - *Step A:* Remove the mean (center at zero).
   - *Step B:* Divide by the standard deviation.
   - *Step C:* Calculate the intercept separately as $\bar{y}$ (the sample mean of the response variable).

------

## 6. Principal Component Regression (PCR) vs. Partial Least Squares (PLS)

### PCR (Principal Component Regression) - *Unsupervised feature extraction*

- **How it works:** Transforms original predictors $X$ into independent Principal Components (PCs) sorted by variance. You drop the lowest-variance PCs to reduce dimensions, then run OLS on the remaining PCs.
- **The Flaw:** PCs are generated using **only $X$**. It ignores the response variable $Y$. The directions in $X$ with the most variance are not necessarily the directions that best predict $Y$.

### PLS (Partial Least Squares) - *Supervised feature extraction*

- **How it works:** Addresses PCR's flaw by using $Y$ to guide the dimension reduction. It identifies linear combinations of $X$ that have high variance *and* are highly correlated with $Y$.
- **Algorithm Steps:**
  1. Standardize variables (mean 0, variance 1). Set initial $Y^{(0)}$ and $X^{(0)}$.
  2. For iteration $m = 1 \dots p$:
     - Calculate weights ($\phi$) using the inner product (covariance) between each predictor $X_j$ and $Y$.
     - Create the latent variable $Z_m = \sum \phi_{mj} X_j$.
     - Regress $Y$ onto $Z_m$ to get a coefficient ($\theta_m$).
     - Update $Y$: $Y^{(m)} = Y^{(m-1)} + \theta_m Z_m$.
     - **Update X (Calculate Residuals):** Regress $X$ onto $Z_m$. Subtract this model output from current $X$ to get the residuals. Use these residuals as the new $X$ for the next iteration.
  3. Use cross-validation to decide how many $m$ iterations (latent components) to keep for the lowest error.



# 4/6 Lecture

------

## Introduction to Support Vector Machines (SVM)

SVM is a family of models used for classification problems. It represents a progression from a simple baseline model to a highly flexible, complex one capable of handling non-linear data.

**Previous Classification Methods Learned:**

- Logistic Regression
- Linear Discriminant Analysis (LDA)
- Quadratic Discriminant Analysis (QDA)
- Naive Bayes Classifier
- Tree Methods (Bagging, Random Forest, Boosting)

**The SVM Family Progression:**

1. **Maximal Margin Classifier:** The simplest, foundational concept.
2. **Support Vector Classifier:** Adds flexibility for messy data.
3. **Support Vector Machine:** Adds the ability to handle non-linear boundaries.

------

## 1. The Hyperplane & Maximal Margin Classifier

The goal of the foundational model is to perfectly split a dataset into two classes using a flat boundary called a hyperplane.

### Hyperplane Basics

- In $p$-dimensional space, a hyperplane is a flat subspace of dimension $p-1$.
- In 2D space, it is a line: $\beta_0 + \beta_1 X_1 + \beta_2 X_2 = 0$
- In 3D space, it is a plane: $\beta_0 + \beta_1 X_1 + \beta_2 X_2 + \beta_3 X_3 = 0$
- Points on one side of the hyperplane yield a result $>0$, while points on the other yield $<0$.
- By labeling the two classes as $1$ and $-1$ (response variable $y_i$), we can combine the condition for correct classification into a single mathematical rule: $y_i(\beta_0 + \beta_1 x_{i1} + \dots + \beta_p x_{ip}) > 0$

### Maximal Margin Classifier Definition

If data can be perfectly separated, there are infinite possible hyperplanes. The **Maximal Margin Classifier** identifies the optimal hyperplane by maximizing the "margin."

- **Margin ($M$):** The minimum perpendicular distance from the separating hyperplane to the nearest training observations.
- **Support Vectors:** The specific data points that lie exactly on the margin boundary. They alone dictate the position of the hyperplane; moving other data points does not affect the model.

### Optimization Model

To find this optimal boundary, the algorithm solves an optimization problem:

- **Objective:** Maximize $M$
- **Constraint 1 (Unit Vector):** $\sum \beta_j^2 = 1$ (Ensures a unique mathematical solution).
- **Constraint 2 (Correct Classification):** $y_i(f(x_i)) \geq M$ (Ensures all points are on the correct side and outside the margin).

### Limitations

- **High Variance:** Hyper-sensitive to single data points changing.
- **Strictly Linear:** Cannot handle curved boundaries.
- **Requires Perfect Separability:** Fails completely if classes overlap.

------

## 2. Support Vector Classifier (Soft Margin)

Real-world data is rarely perfectly separable. The Support Vector Classifier introduces a **Soft Margin** to allow for a more robust model that tolerates some misclassifications in exchange for better overall prediction.

### Slack Variables ($\epsilon_i$)

Slack variables measure the distance of a point's violation across the margin or hyperplane.

- $\epsilon_i = 0$: Observation is on the correct side of the margin.
- $\epsilon_i > 0$: Observation violated the margin but is still on the correct side of the hyperplane.
- $\epsilon_i > 1$: Observation crossed the hyperplane entirely (misclassified).

### The Tuning Parameter ($C$)

A new constraint limits the total allowable violations: $\sum \epsilon_i \leq C$

- **$C$ limits total errors:** It dictates how many points can violate the margin or hyperplane.
- **Small $C$:** Narrow margin, tolerates fewer violations, low bias, high variance (overfits).
- **Large $C$:** Wider margin, tolerates more violations, higher bias, lower variance (more robust).

------

## 3. Support Vector Machine (The Kernel Trick)

When the boundary between classes is inherently non-linear, a linear plane will fail. The full Support Vector Machine solves this by mapping data into a higher-dimensional space where a linear cut *can* be made.

### The Problem with Polynomial Expansion

You could manually enlarge the feature space (e.g., adding $X_1^2$, $X_2^3$). However, this drastically increases the number of coefficients required, making computation intractable for large datasets.

### The Kernel Approach

Instead of explicitly enlarging the feature space, SVM uses a **Kernel Function** to replace the inner product calculations between pairs of observations.

- Only **Support Vectors** have non-zero coefficients ($\alpha_i$). Non-support vectors mathematically drop out, drastically reducing computation.
- **Polynomial Kernel:** Uses a degree parameter ($d$) to simulate higher polynomial spaces.
- **Radial Kernel (RBF):** Calculates Euclidean distance between points and applies a negative exponential. It has "local behavior"—distant training observations mathematically approach zero and play essentially no role in predicting a new observation's class.

### Visualizing the Kernel Trick

Imagine data plotted on a flat, 2D rubber sheet that cannot be separated by a straight line. The Kernel Trick mathematically "bends and stretches" this sheet into a 3D space. Once warped, a single, flat slice (hyperplane) can easily separate the classes. When you un-warp the sheet back to 2D, the straight cut translates into a complex, non-linear boundary around your data.

------

## 4. Multi-Class SVM

Standard SVM only splits data into two classes. To handle $>2$ classes ($k$), two primary workarounds are used:

| **Approach**             | **Description**                                              | **Final Decision Rule**                                      |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **One-Versus-One (OvO)** | Constructs a separate SVM model for every possible pair of classes. Total models = $\binom{k}{2}$. | A new observation is tested on all models. The class that wins the most "votes" is the final prediction. |
| **One-Versus-All (OvA)** | Constructs $k$ models. Each model compares one specific class against all remaining classes grouped together. | A new observation is tested on all models. The model outputting the highest confidence value determines the class. |

Here is a detailed, cheatsheet-style lecture note based on your transcript. I've structured it to prioritize quick scanning, mathematical clarity, and core concepts.



# 4/8 Lecture - Neural Networks

## 1. High-Level Overview & Applications

Neural Networks (NNs) are powerful predictive analytics tools used to model complex, non-linear relationships by learning from large datasets.

- **Predictive Analytics & Forecasting:** Weather forecasting, traffic volume prediction.
- **Computer Vision (CNNs):** Medical image diagnosis (CT scans), License plate recognition (Intelligent Transportation Systems), Facial recognition, Autonomous driving (Tesla, Waymo object detection).
- **Natural Language Processing (LLMs):** Information surfacing and conversational AI (e.g., ChatGPT).

------

## 2. Anatomy of a Single Neuron (The Operator)

A single neuron acts as a computational unit (an "operator"). Information always flows from **left to right** (Feedforward).

### **The Computation Steps:**

1. **Input Vector ($X$):** Raw inputs enter from the left: $x_1, x_2, \dots, x_n$.

2. **Weights ($\omega$):** Every input is multiplied by a corresponding weight.

3. **Bias ($\beta_0$ or $\omega_0$):** An intercept term is added (similar to linear regression).

4. **Aggregation:** The neuron calculates the weighted sum:

   $$z = \sum_{i=1}^{n} (\omega_i \cdot x_i) + \text{bias}$$

5. **Activation Function ($g(z)$):** The aggregated sum is passed through a non-linear function to generate the final output (called the **Activation**, denoted as $a$).

### **Common Activation Functions:**

- **Sigmoid / Logistic:** Outputs values between 0 and 1 (often used for probabilities).

- **Hyperbolic Tangent (Tanh):** Outputs values between -1 and 1.

- **ReLU (Rectified Linear Unit):** Extremely common in modern NNs.

  $$g(x) = \max(0, x)$$

  *(If $x$ is negative, output is 0; if positive, output is $x$)*

- **Softmax:** Used in the output layer for multi-class classification to generate a probability distribution.

------

## 3. Network Architecture (Multilayer Perceptron - MLP)

Neurons are stacked into layers to create a network.

- **Input Layer:** Takes the raw data. (No activation functions applied here; acts as a pass-through).
- **Hidden Layer(s):** The intermediate layers where the core feature extraction and non-linear transformations happen.
- **Output Layer:** Generates the final prediction.
- **Fully Connected:** Every neuron in a given layer connects to *every* neuron in the subsequent layer. There are **no connections** between neurons within the same layer.
- **Weight Matrices:** The weights between layers are stored mathematically as matrices. A network with 3 layers (Input, 1 Hidden, Output) requires **2 weight matrices**.

> **💡 The Universal Approximation Theorem:**
>
> In theory, a neural network with just **one single hidden layer** containing a sufficient number of neurons can approximate almost any continuous function. However, using two or more hidden layers can often achieve the same result faster and with fewer total neurons, reducing the risk of overfitting.

------

## 4. Mathematical Representation & Training

A neural network is essentially a massive set of **nested functions**.

### **Feedforward Propagation Model**

For a simple network with one hidden layer:

$$f(X) = \sum_{k} \alpha_k \cdot g\left(\sum_{i} \omega_{ik}x_i + \text{bias}_k\right) + \text{bias}_{out}$$

- $\omega$: Weights from Input $\rightarrow$ Hidden Layer.
- $\alpha$ (or $\beta$): Weights from Hidden $\rightarrow$ Output Layer.

### **Model Training**

"Training" a network means finding the optimal numerical values for the weight matrices and biases. This is framed as an optimization problem:

1. **Regression Problems:** Minimize the Sum of Squared Errors (SSE).

   $$\text{Minimize: } \sum (y_i - f(x_i))^2$$

2. **Classification Problems:** Maximize the Log-Likelihood (or minimize the Negative Log-Likelihood/Cross-Entropy).

------

## 5. Case Study: MNIST Digit Classification

How images are transformed into mathematical inputs:

- **Goal:** Classify handwritten digits (0-9).
- **Data Size:** 60,000 images.
- **Digitalization:** A $28 \times 28$ pixel image is flattened into a single vector of **784 elements**.
- **Architecture Sizing Example:**
  - **Input Layer:** 784 neurons (one for each pixel).
  - **Hidden Layer 1:** 256 neurons. *(Weight Matrix 1 Size: $785 \times 256$, including bias)*
  - **Hidden Layer 2:** 128 neurons. *(Weight Matrix 2 Size: $257 \times 128$)*
  - **Output Layer:** 10 neurons (one for each digit 0-9). *(Weight Matrix 3 Size: $129 \times 10$)*

------

## 6. Calculation Walkthrough (The $X_1 X_2$ Problem)

This is the specific mathematical example the professor walked through manually on the board to prove how NNs capture non-linear interactions.

**Given Parameters:**

- Inputs: $p=2 \implies (x_1, x_2)$
- Hidden Nodes: $k=2 \implies (h_1, h_2)$
- Activation Function: $g(z) = z^2$
- Weights to Hidden ($\omega$): $w_{11}=1, w_{12}=1, w_{21}=1, w_{22}=-1$
- Weights to Output ($\alpha$): $\alpha_1=\frac{1}{4}, \alpha_2=-\frac{1}{4}$
- Biases: All $0$

**Step-by-Step Propagation:**

1. **Hidden Node 1 ($h_1$):**
   - Weighted sum: $(1\cdot x_1) + (1\cdot x_2) = x_1 + x_2$
   - Activation: $a_1 = (x_1 + x_2)^2$
2. **Hidden Node 2 ($h_2$):**
   - Weighted sum: $(1\cdot x_1) + (-1\cdot x_2) = x_1 - x_2$
   - Activation: $a_2 = (x_1 - x_2)^2$
3. **Final Output ($o_1$):**
   - $f(X) = \frac{1}{4}a_1 - \frac{1}{4}a_2$
   - $f(X) = \frac{1}{4}(x_1^2 + 2x_1x_2 + x_2^2) - \frac{1}{4}(x_1^2 - 2x_1x_2 + x_2^2)$
   - **Result:** $f(X) = x_1x_2$



# 4/13 Lecture - Neural Networks: Architecture & Training Cheatsheet

## 1. Architecture & Core Concepts

A neural network maps an input space to an output space via non-linear transformations. Its capacity is defined by its architecture and the data it is trained on (e.g., supervised learning using image, traffic, or text data).

- **Input Layer:** Takes raw data. No activation functions or aggregations occur here.
  - *Example (MNIST Handwritten Digits):* A 28x28 pixel image is flattened into a single vector of $784$ elements, requiring $784$ input neurons.
- **Hidden Layer(s):** Intermediate layers where weighted sums are calculated and passed through activation functions.
- **Output Layer:** Generates the final model predictions.
- **Weight Matrices ($\omega$ or $\theta$):** The connections between layers. Training a network is fundamentally the process of finding the optimal values for these matrices.

## 2. Feedforward Propagation (The Forward Pass)

The process of passing data from the input layer to the output layer to generate a prediction.

**Step 1: Calculate Weighted Sums**

For each neuron $j$ in the hidden layer, calculate the sum of the inputs multiplied by their corresponding weights:

$x_j = \sum (y_i \cdot \omega_{ij})$

*(Where $y_i$ is the output from the previous layer, and $\omega_{ij}$ is the connecting weight).*

**Step 2: Apply Activation Function**

Plug the weighted sum into an activation function $g()$ to get the neuron's output (activation):

$y_j = g(x_j)$

*(Example: The Sigmoid/Logistic function).*

**Step 3: Generate Output Probabilities (Softmax)**

For classification tasks (like the 10-digit MNIST problem), the raw output of the final layer ($z$) is converted into probabilities using the **Softmax function**:

$P(class = m | x) = \frac{e^{z_m}}{\sum_{i=1}^{10} e^{z_i}}$

The model classifies the input as the digit with the highest resulting probability.

------

## 3. Model Estimation (Training)

The essence of training is adjusting weight matrices so the model output ($\hat{y}$) is as close as possible to the target/observed value ($y$).

- **Objective Function:** We measure the discrepancy using Sum of Squared Errors (SSE):

  $E = \sum (y_{target} - \hat{y}_{model})^2$

- **Optimization Problem:** We aim to minimize this objective function.

- **Non-Convexity:** Unlike linear regression, neural network optimization is non-convex. The searching domain has many "valleys" (local optima). Gradient descent typically finds a **local optimum**, not the global optimum. Different starting initializations will result in different local optima.

## 4. Gradient Descent Algorithm

An iterative optimization method used to find the minimum of the objective function.

**Algorithm Steps:**

1. **Initialize Parameters:** Start with random guess values for all weight matrices (e.g., random values between $0$ and $1$). Set iteration $t = 0$.

2. **Calculate Gradient ($\Delta$):** Determine the gradient (partial derivative) of the objective function with respect to the weights.

3. **Update Weights:** Adjust the current weight using the gradient and a learning rate ($\rho$):

   $\theta_{t+1} = \theta_t - \rho \cdot \Delta$

4. Repeat until the error stops significantly decreasing.

**The Learning Rate ($\rho$):** A tuning parameter (usually between $0$ and $1$) that controls step size.

- **Too large:** You may overshoot the optimal solution.
- **Too small:** High probability of hitting the optimum, but requires vastly more iterations (longer training time).

------

## 5. Backward Propagation (Backprop)

The process of going backward (from output to input) to distribute the total error into small pieces (gradients) for every single weight. It uses the **Chain Rule** from calculus.

### Updating Hidden-to-Output Weights ($\omega_{jk}$)

To find how much a specific weight between the hidden layer ($j$) and output layer ($k$) contributed to the total error ($E$):

$\frac{\partial E}{\partial \omega_{jk}} = \frac{\partial E}{\partial y_k} \cdot \frac{\partial y_k}{\partial x_k} \cdot \frac{\partial x_k}{\partial \omega_{jk}}$

- $\frac{\partial E}{\partial y_k}$: Derivative of the error function.
- $\frac{\partial y_k}{\partial x_k}$: Derivative of the activation function (e.g., for sigmoid, this is $y_k(1 - y_k)$).
- $\frac{\partial x_k}{\partial \omega_{jk}}$: Derivative of the weighted sum, which simplifies to the activation from the previous node ($y_j$).

### Updating Input-to-Hidden Weights ($\omega_{ij}$)

When moving further back to weights between the input ($i$) and hidden layer ($j$), the chain rule must account for the fact that a single hidden neuron ($j$) contributes to **every** neuron in the output layer ($k$). We must sum these pathways:

$\frac{\partial E}{\partial \omega_{ij}} = \left( \sum_k \frac{\partial E}{\partial x_k} \cdot \frac{\partial x_k}{\partial y_j} \right) \cdot \frac{\partial y_j}{\partial x_j} \cdot \frac{\partial x_j}{\partial \omega_{ij}}$

------

## 6. Network Design, Pros, & Cons

### Hyperparameters & Architecture

- **No theoretical formula** exists to perfectly determine the number of hidden layers or neurons.
- **Rule of Thumb:** A single hidden layer with a neuron count equal to $2/3$ of the sum of the input and output neurons.
- **Multiple Hidden Layers:** Used in practice to shorten the time it takes to find a solution.
- **Learning Rate:** Often determined via cross-validation.

### Advantages

- Excellent at capturing complex, non-linear mappings.
- Strong anti-noise capacity (though bounded by "garbage in, garbage out").

### Disadvantages

- **Black Box:** No statistical diagnosis or inference. You cannot interpret the meaning of individual weights or calculate confidence intervals (unlike regression coefficients).
- **Overfitting:** A major risk. The model can memorize training data and fail on unseen data.

### Preventing Overfitting

1. **Cross-Validation:** Split data into training, validation, and testing sets. Use validation to know when to stop training (Early Stopping).
2. **Regularization:** Penalize overly complex weights.
3. **Slow Learning Rate:** Use a smaller $\rho$.



# 4/15 Lecture - Neural Networks & Deep Learning

## Part 1: Training & Mitigating Overfitting

Overfitting occurs when a neural network memorizes training data but fails to generalize to new data. You cannot 100% prevent it, but you can mitigate it.

### 🛡️ Strategies to Prevent Overfitting

- **Slowing Learning Rate:** Reduces the step size during weight adjustments. It takes longer to converge to a local optimum but can yield better generalization.
- **Regularization (Ridge/Lasso style):** Adding a penalty term to the objective function (e.g., squaring or taking the absolute value of all weight matrices and summing them). This forces less important weights towards zero, highlighting the most significant parameters.
- **Dropout Learning:**
  - **Mechanism:** Randomly select a percentage of neurons (the *dropout rate*, e.g., 10%) to ignore during a single feedforward pass (their input/output becomes zero).
  - **Purpose:** Prevents the network from relying too heavily on a few "strong" neurons.
  - **Analogy:** Similar to Random Forest in decision trees, where random subsets of predictors are used so every feature gets an equal chance to contribute.

### ⚙️ Training Mechanics & Terminology

- **Feedforward Propagation:** Passing input data layer-by-layer from left to right to get an output and calculate the total error.
- **Backward Propagation:** Redistributing that total error backwards through the network to adjust the weight matrices.
- **Stochastic Gradient Descent (SGD):** An algorithm for optimizing weights using batches rather than the whole dataset at once.
  - **Mini-Batch:** A subset of the training data (e.g., batch size of 128). The network does feedforward 128 times, accumulates the total error, and then does **one** backward propagation to adjust weights.
  - **Epoch:** One complete cycle where the entire training dataset has been processed.
  - *Example:* If you have 48,000 training images and a batch size of 128, you will perform 375 backward propagations per epoch ($48,000 / 128 = 375$).
- **Data Splits:** A common split is 80% training data and 20% validation data. The validation set is used to determine when to stop training (via cross-validation curves).

### 🎛️ Hyperparameters to Tune

Hyperparameters are set before training begins and dictate the network structure and learning process:

- Number of hidden layers & neurons per layer
- Learning rate ($\rho$)
- Regularization penalty
- Dropout rate
- Optimization algorithm (e.g., SGD)
- Mini-batch size & Number of epochs

### 🐍 Python Packages for Neural Networks

- **Scikit-Learn:** Simpler package with built-in datasets; good for basic models.
- **TensorFlow:** Industry-standard, highly flexible, but has complex syntax.
- **Keras:** A highly user-friendly interface that runs TensorFlow under the hood.
- **PyTorch:** Another professional library (though noted as occasionally complex to configure).

------

## Part 2: Deep Learning & Convolutional Neural Networks (CNNs)

**Deep Learning Definition:** A neural network containing **two or more hidden layers**. Because each layer acts as a linear combination passed through transformations, stacking them helps capture complex non-linearities.

### 👁️ Convolutional Neural Networks (CNN) Overview

Primarily used for computer vision, image classification, and object recognition (e.g., autonomous vehicles recognizing stop signs). CNNs map visual features to class labels (e.g., "Tiger" or "Car").

#### 1. Image Pre-processing (Digitalization)

Computers cannot "see" colors. Images are converted into a 3D **Tensor** consisting of three matrices corresponding to fundamental color channels: **Red, Green, and Blue (RGB)**. The numerical values represent pixel intensity.

#### 2. Operation A: Convolution

- **The Filter:** A small matrix (e.g., 2x2 or 3x3) containing a specific numerical pattern (weights) designed to extract a specific feature (vertical lines, horizontal lines, etc.).
- **The Process:** 1. Place the filter on the top-left of the image matrix.
  2. Multiply corresponding elements and sum the products to create a single new value.
  3. Shift the filter across the image.
- **Stride:** The number of pixels the filter shifts at a time (e.g., a stride of 2 means shifting 2 columns over).
- **Padding:** Adding blank rows/columns to the margins of the original matrix to ensure the filter fits perfectly during shifts.
- **The Output (Feature Map):** Because the original image has 3 channels, the filter must also have 3 channels. The results of the 3 filter applications are summed into a single 2D matrix called a **Feature Map**.
- *Note:* Applying $K$ different filters results in $K$ feature maps (a new 3D tensor).
- **Advantage of Convolution:** Reduces the total number of parameters (compared to standard neural networks) while preserving the "local spatial relationships" (relative positions) of the pixels.

#### 3. Activation: ReLU

After convolution, the feature maps pass through a **ReLU (Rectified Linear Unit)** activation function:

- Positive inputs remain unchanged.
- Negative inputs become 0.

#### 4. Operation B: Pooling

- **Purpose:** To reduce dimensionality while keeping the most significant extracted features.
- **Max Pooling:** Places a small grid (e.g., 2x2) over the feature map and extracts only the maximum value in that area. (Results in some information loss, but massive efficiency gains).
- **Average Pooling:** Takes the average of the values in the grid.

#### 5. Data Augmentation

To train CNNs effectively without gathering millions of new photos, existing images are augmented. You rotate, flip, mirror, or change the angle of a base image. This trains the computer to recognize the object regardless of its orientation.

#### 6. The Final Architecture: Fully Connected Layer (FC)

1. You repeat Convolution -> ReLU -> Pooling multiple times until the matrices are very small.
2. **Flattening:** You stack the columns of all remaining small matrices into one massive, 1-dimensional vector.
3. This vector is fed into a standard, **Fully Connected (FC) Neural Network**.
4. **Softmax Output:** The final layer uses a Softmax function to convert the final node values into **probabilities** (e.g., an 85% chance the image belongs to the "Tiger" class).





# 4/20 Lecture - Deep Learning: Recurrent Neural Networks & Beyond

## 1. Sequential Data Fundamentals

Recurrent Neural Networks (RNNs) are specially designed to handle **sequential data** where the order of observations matters due to the correlation between neighboring data points.

- **Examples of Sequential Data:**
  - **Text/Documents:** Books, movie reviews, language. Word order dictates meaning.
  - **Time-Series Data:** Weather forecasting, stock prices (financial time-series). Data changes dynamically over time.
  - **Media:** Video, audio, music. Reordering frames or notes destroys the content.
- **Stationary vs. Non-Stationary Data:** 
  - Raw time-series data often has changing variance over time (*heteroscedasticity*), making it non-stationary.
  - To build a stable model, you must convert it to **stationary data** (e.g., by taking the log of the values to stabilize the variance).

## 2. Recurrent Neural Networks (RNN) Architecture

An RNN can be visualized as multiple "mini" neural networks (columns) connected sequentially.

- **The Core Mechanism:**
  - Unlike standard networks, the hidden layers of an RNN are connected to each other across time steps.
  - The input to a hidden layer at time $t$ is a combination of the **raw input at time $t$** AND the **output (activation) from the hidden layer at time $t-1$**.
  - This allows the network to accumulate historical information as it moves forward.
- **Shared Matrices:** Despite having many "mini" networks, an RNN only estimates **three shared weight matrices**:
  1. Input to Hidden Layer ($W$)
  2. Hidden Layer to next Hidden Layer ($U$)
  3. Hidden Layer to Output Layer ($V$)
- **Determining Sequence Length ($L$ / Lag):**
  - How many past steps should you use to predict the future? Use the **Autocorrelation Function (ACF)**.
  - ACF measures the correlation between observations at different time gaps (lags). If the gap is small, correlation is usually high; as the gap grows, correlation weakens.
  - *Example:* If autocorrelation is strong up to a gap of 5 days, you set your sequence length to $L=5$.

## 3. Limitations of RNNs & The LSTM Solution

Standard RNNs struggle with two major problems during backward propagation:

1. **Vanishing / Exploding Gradients:** Gradients can approach zero (weights stop updating) or approach infinity (model breaks).
2. **Long-Term Dependency:** As the sequence gap grows, the RNN fails to connect relevant information from the far past to the present.

### Long Short-Term Memory (LSTM)

- LSTMs are a specialized, improved version of RNNs designed to solve the above problems (analogous to how Random Forest improves upon standard Bagging).
- **How it works:** It uses **two parallel lines/tracks** in the hidden layer. One track captures information from the *further past* (long-term memory), and the other captures information from the *recent past* (short-term memory).

## 4. Alternative Architectures for Time-Series

### Elman Neural Network

- Introduces a **Context Layer**.
- **Mechanism:** It makes a copy of the activation from the **hidden layer** and saves it in the context layer. In the next time step, the new input combines with this saved context layer information before entering the hidden layer.

### Jordan Neural Network

- Also uses a Context Layer, but with a key difference in what it saves.
- **Mechanism:** Instead of saving the hidden layer's activation, it makes a copy of the **final model output** and saves it to the context layer to be used in the next iteration.

## 5. Restricted Boltzmann Machines (RBM)

A generative model used to estimate probability distributions.

- **Structure:** Contains only two layers: a **Visible Layer** ($v$) and a **Hidden Layer** ($h$).
- **Key Features:**
  - Neurons only take binary values ($0$ or $1$).
  - Connections between layers are **bidirectional**.
- **Mechanism:** Different binary combinations represent different events. It calculates the probability of an event using a **Softmax function** applied to an **Energy function** ($E$).

## 6. Data Preprocessing: Standardization

> **Critical Rule:** Never feed raw, unstandardized data into a neural network. It will not work properly.

Always preprocess your features using one of these common formulas:

- **Min-Max Scaling:** Scales values between 0 and 1.

  $$x_{scaled} = \frac{x - x_{min}}{x_{max} - x_{min}}$$

- **Z-Score Normalization:** Centers data around a mean of 0 with a standard deviation of 1.

  $$x_{scaled} = \frac{x - \mu}{\sigma}$$

## 7. Model Selection & The Parsimony Principle

Neural Networks are powerful, but they shouldn't be used for everything.

- **The Parsimony Principle:** If multiple models yield similar accuracy, always choose the **simplest model** (e.g., Linear Regression or Lasso over a Neural Network).
- **Why?** Simpler models are faster to run and easier to interpret. NNs require immense effort to fine-tune hyperparameters (number of hidden layers, neurons, learning rate) and are computationally expensive.
- **When to use NNs:** Reserve Deep Learning for extremely large, highly complex datasets where simpler models fail to capture the underlying patterns.

------

### 📌 Course Admin Notes

- **Homework 6:** Focuses on setting up and running models on the High-Performance Computing (HPC) facility. It is treated as a **bonus**. You must generate a reasonable, real result to get the extra credit (no points just for logging in).
- **Final Exam:** Wednesday, April 29th during normal class time. In-person, open-book. Same format and style as the midterm (no coding required).
- **Review Session:** Next Monday.



# 4/22 Lecture - CRAC High Performance Computing (HPC)

> Step-by-step setup for the Discovery cluster at USC's Center for Advanced Research Computing (CARC). Follow in order — do **not** skip ahead.

---

## 0. Prerequisites & Files to Download

### From Brightspace → HPC files folder, download ALL of these:
| File | Purpose |
|---|---|
| `VPN` (Windows installer) | Cisco VPN — only needed for Windows users from home |
| `WinSCP` | File transfer software (Windows) |
| `FileZilla` | File transfer software (Mac) |
| `.bashrc` | Backup config file — only needed if Conda fails to auto-create one |
| 4 Python example files | CNN (MNIST), RNN, SVM, etc. — templates for HW6 |
| SLURM file | Job submission script (**critical** — easy to miss) |

### Verify access to professor's project:
- Log into the CARC user portal → choose **University of Southern California** → continue.
- Confirm your name is listed as a member of the professor's project.
- If not listed, notify the professor.

---

## 1. Network Connection (REQUIRED before login)

| Where you are | What you need |
|---|---|
| **On campus** | Connect to **USC Secure** Wi-Fi (NOT "USC Guest" — guest will not work) |
| **From home** | Install & start **USC VPN (Cisco AnyConnect)** before SSH |

### Installing VPN
- **Mac:** Click the VPN link → log in with USC credentials → site auto-detects Mac → download → install.
- **Windows:** Use the VPN installer from Brightspace → unzip → install.

### Starting VPN (from home)
1. Open Cisco AnyConnect.
2. Enter VPN address: `vpn.usc.edu`
3. Click **Connect** → log in with USC username/password.
4. Once connected, your laptop appears as an on-campus machine to HPC. Without this, HPC will reject your connection.

---

## 2. SSH Login to Discovery

Open a terminal (Mac: Terminal app | Windows: right-click → terminal / use PowerShell).

```bash
ssh your_username@discovery.usc.edu
```

- Replace `your_username` with **your** USC username (NOT the professor's).
- If hostname fails on Mac, try the **IP address** instead of `discovery.usc.edu`.
- First time: prompt asks "Are you sure you want to continue connecting?" → type `yes`.
- Enter password — **it is invisible** (no asterisks, no dots). Just type it and press Enter.
- **No copy-paste for the password.** Type it manually.
- Use the **same password as your USC/Brightspace account**.

✅ Success looks like: `(base) your_username@discovery2:~$` (or similar with `discovery2`).
❌ If you still see your local machine prompt, you are NOT logged in.

> If `ssh` "connection timed out" → check Wi-Fi is USC Secure (not guest), or VPN is on if at home.

---

## 3. Install Miniconda

Run the **three commands line-by-line** from the lecture file (do NOT paste all at once).

```bash
# Line 1 — downloads installer
# Line 2 — chmod / makes it executable
# Line 3 — runs the installer
```

### During the installation prompts:
| Prompt | What to do |
|---|---|
| License agreement | Press Enter to scroll → type `yes` to accept |
| Confirm install location | Press **Enter** to accept default |
| **"Do you wish to update your shell profile to automatically initialize conda?"** | **Type `yes`** ⭐ THIS IS CRITICAL |

> ⚠️ If you accidentally typed `no` → you must manually fix `.bashrc` (see Section 3b).

### After install completes:
```bash
exit                         # log out
ssh your_username@discovery.usc.edu  # log back in
```

You should now see `(base)` at the front of your prompt.

Test:
```bash
conda --version
```

---

## 3b. Fixing a Missing `.bashrc` (only if you said "no" above)

Symptom: `conda` command does nothing, no `(base)` prefix, `ls -la` shows no `.bashrc` file.

1. Download `.bashrc` from Brightspace HPC folder → **unzip it**.
2. **Mac users**: `.bashrc` is a hidden file → enable "Show hidden files" in Finder (`Cmd + Shift + .`).
3. Open `.bashrc` in a text editor:
   - Windows: Right-click → Open with → Notepad
   - Mac: Open with TextEdit (plain text mode)
4. **Find every instance of the professor's username and replace with YOUR username.** Do not touch anything else.
5. Save the file.
6. Transfer `.bashrc` to your HPC home directory using WinSCP / FileZilla (see Section 5).
7. On HPC, run:
   ```bash
   ls -la                  # confirm .bashrc is there
   nano .bashrc            # optional: verify contents
   source ./.bashrc        # apply config
   conda --version         # should now work
   ```

---

## 4. Create Virtual Environment + Install Python

### Verify platform first:
```bash
conda info
```
Look at the bottom — **platform should be `linux-64`**. If it isn't, tell the professor.

### Create the env:
```bash
conda create --platform linux-64 --name py310
```
- Type `y` when prompted to proceed.

### Verify it was created:
```bash
conda env list
```
You should see two entries: `base` and `py310`.

### Activate it:
```bash
conda activate py310
```
Prompt should now show `(py310)` instead of `(base)`. **Always work inside `py310`** — never install into `base`.

### Install Python 3.10 (REQUIRED — TensorFlow needs this version):
```bash
conda install python==3.10
```
- Do **not** install 3.11/3.12/3.13 — incompatible with TensorFlow.
- Verify:
  ```bash
  python --version    # should show Python 3.10.x
  python              # opens REPL
  >>> exit()          # leave REPL
  ```

### Install Python libraries
Run **line-by-line** from the lecture file (each library install command separately).

---

## 5. File Transfer Setup (Local ↔ HPC)

### Windows → install **WinSCP**
1. Download from Brightspace → unzip → double-click installer.
2. Open WinSCP → **New Session**:
   - Host name: `discovery.usc.edu`
   - Port: `22`
   - Username + password: your USC credentials
3. Accept host key → log in.
4. Layout: **Left pane = your laptop, Right pane = HPC.** Drag files between them.

### Mac → install **FileZilla**
1. Download from Brightspace → install.
2. New connection → host: `discovery.usc.edu`, your credentials, port 22 → connect → trust host.
3. Same drag-and-drop interface.

---

## 6. Submitting a Job (SLURM)

### Transfer the example Python files + SLURM file from local to HPC
Use WinSCP/FileZilla.

### Edit the SLURM file
Open it on HPC with nano:
```bash
nano slurmfile_name
```

**Edit these things:**

- ✅ Replace the **folder name / username** in the file with YOUR username.
- ❌ Do **NOT** change the **project ID / account** line — that's the professor's project; the system only accepts jobs under it.
- ⚠️ Use **hyphens (`-`)**, not underscores (`_`), where the template uses hyphens.

Save in nano: `Ctrl + X` → `Y` → Enter.

### Submit the job:
```bash
sbatch slurmfile_name
```

### Check results:
```bash
ls -la
```
Look for new output files — e.g. PNG plots, log files, `.out` files.

### Pull results back to your laptop
Use WinSCP/FileZilla → drag output file from right (HPC) to left (local) → open it locally.

---

## 7. Quick Command Reference

| Task | Command |
|---|---|
| SSH to HPC | `ssh user@discovery.usc.edu` |
| Reload shell config | `source ~/.bashrc` |
| Conda version | `conda --version` |
| List envs | `conda env list` |
| Create env | `conda create --platform linux-64 --name py310` |
| Activate env | `conda activate py310` |
| Deactivate env | `conda deactivate` |
| Install Python 3.10 | `conda install python==3.10` |
| Submit SLURM job | `sbatch <slurmfile>` |
| List files (incl. hidden) | `ls -la` |
| Edit a file | `nano <filename>` |
| Save in nano | `Ctrl+X` → `Y` → Enter |
| Exit Python REPL | `exit()` |
| Logout | `exit` |

---

## 8. Common Pitfalls (don't do these)

- ❌ Pasting all 3 Miniconda commands at once — run line by line.
- ❌ Saying "no" to the conda shell-init question (creates the `.bashrc` problem).
- ❌ Working in `(base)` — always activate `py310` first.
- ❌ Installing Python 3.11+ — TensorFlow needs **3.10**.
- ❌ Trying to copy-paste your password during SSH — type it.
- ❌ Connecting to "USC Guest" Wi-Fi — won't reach HPC.
- ❌ Editing the project/account ID in the SLURM file — only edit folder/username paths.
- ❌ Using underscores where the template uses hyphens in SLURM.
- ❌ Forgetting to start VPN when working from home.

---

## 9. Bonus HW6 Notes
- Examples provided: **CNN on MNIST** (60k handwritten digit images), **RNN**, **SVM**.
- Use these as templates for HW6; modify with ChatGPT/Google for additional pieces as needed.
- HW6 is bonus — completing it adds extra credit and the experience is a strong **resume bullet** ("hands-on with HPC cluster computing").