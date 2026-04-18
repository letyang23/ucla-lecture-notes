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