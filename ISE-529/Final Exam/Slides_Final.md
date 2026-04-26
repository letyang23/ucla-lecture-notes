# 7. Tree-Based Methods (I)

##### Outline

- Build a decision tree
- Regression trees
- Classification trees
- Bagging, Random Forests (RF), Boosting

## **TREE-BASED METHODS**

# Tree-Based Methods

- Tree-based methods can be applied to both regression and classification problems.
- These involve *stratifying* or *segmenting* the predictor space into a number of simple regions.
- To make a prediction for a given observation, we typically use the mean or the mode response value for the training observations in the region to which it belongs.
- Since the set of splitting rules used to *segment* the predictor space can be summarized in a *tree*, these types of approaches are known as *decision-tree* methods.

- Tree-based methods are simple and useful for interpretation. However, they typically are not competitive with the best supervised learning approaches in terms of prediction accuracy.
- Hence, we also discuss *bagging*, *random forests*, and *boosting*. These methods produce multiple trees which are then combined to yield a single consensus prediction.
- Combining a large number of trees can often result in dramatic improvements in prediction accuracy, at the expense of some loss interpretation.

We first consider regression problems, and then move on to classification.

## **BUILD A SIMPLE DECISION TREE**

### Build a Simple Decision Tree

- This example builds classification models in the form of a tree structure.
- It breaks down a dataset into smaller subsets. The final result is a tree with *decision nodes* and *leaf nodes*.
- A decision node has two or more branches. Leaf node represents a classification or decision.
- The *topmost decision node* in a tree which corresponds to the best predictor called *root node*.
- Decision trees can handle both categorical and numerical data.

### Build a Simple Decision Tree

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.06.01 PM.png" alt="Screenshot 2026-04-25 at 3.06.01 PM" style="zoom:50%;" />

### Build a Simple Decision Tree

- The algorithm for building this decision tree proposed by J. R. Quinlan which employs a top-down, greedy search through the space of possible branches with no backtracking.
- The algorithm uses *Entropy and Information Gain* to construct a decision tree.
- Decision tree includes all predictors with the dependence assumptions between predictors.

### Entropy and Information Gain

A decision tree is built top-down from a *root node* and involves partitioning the data into subsets that contain instances with similar values (homogenous).

The algorithm uses **entropy** to calculate the *homogeneity* of a sample.

If the sample is completely homogeneous the entropy is zero and if the sample is an equally divided it has entropy of one.

### Entropy and Information Gain

Calculate *Entropy* using the *frequency table* of **one attribute**:

$$Entropy(S) = \sum_{i=1}^n -p_i \log_2 p_i$$

| Play Golf |    |
|-----------|----|
| Yes       | No |
| 9         | 5  |

$$\begin{aligned} Entropy(\text{Play Golf}) &= Entropy(5,9) \\ &= Entropy(0.36, 0.64) \\ &= -0.36 \log_2(0.36) - 0.64 \log_2(0.64) \\ &= 0.94 \end{aligned}$$

#### More Examples for Entropy

More examples of calculating **Entropy** using the frequency table:

| C1   | <b>0</b> |
| ---- | -------- |
| C2   | <b>6</b> |

$$\begin{aligned} P(C1) &= 0/6 = 0 & P(C2) &= 6/6 = 1 \\ \text{Entropy} &= -0 \log_2(0) - 1 \log_2(1) = -0 - 0 = 0 \end{aligned}$$

| C1   | <b>1</b> |
| ---- | -------- |
| C2   | <b>5</b> |

$$\begin{aligned} P(C1) &= 1/6 & P(C2) &= 5/6 \\ \text{Entropy} &= -(1/6) \log_2(1/6) - (5/6) \log_2(5/6) = 0.65 \end{aligned}$$

| C1   | <b>2</b> |
| ---- | -------- |
| C2   | <b>4</b> |

$$\begin{aligned} P(C1) &= 2/6 & P(C2) &= 4/6 \\ \text{Entropy} &= -(2/6) \log_2(2/6) - (4/6) \log_2(4/6) = 0.92 \end{aligned}$$

### Entropy and Information Gain

Calculate **weighted entropy** using the frequency table of **two attributes**:

$$Entropy(T, X) = \sum_{c \in X} p(c)E(c)$$

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.08.49 PM.png" alt="Screenshot 2026-04-25 at 3.08.49 PM" style="zoom:50%;" />

$$\begin{aligned} &Entropy(T=\text{PlayGolf}, X=\text{Outlook}) \\ &= P(\text{Sunny}) * E(3,2) + P(\text{Overcast}) * E(4,0) + P(\text{Rainy}) * E(2,3) \\ &= (5/14) * 0.971 + (4/14) * 0.0 + (5/14) * 0.971 \\ &= 0.693 \end{aligned}$$

The information gain is based on the decrease in entropy after a dataset is split on an attribute. Constructing a decision tree is all about finding **attribute** (decision nodes) that returns the highest information gain (i.e., the most homogeneous branches).

Step 1: Calculate entropy of the response/target (e.g., Play Golf).

$$\begin{aligned}\text{Entropy}(\text{Play Golf}) &= \text{Entropy}(5,9) \\ &= \text{Entropy}(0.36, 0.64) \\ &= -0.36\log_2(0.36) - 0.64\log_2(0.64) \\ &= 0.94\end{aligned}$$

### Entropy and Information Gain

#### Step 2:

The dataset is then split on the different attributes. Calculate the entropy for each attribute. The resulting **weighted entropy** is subtracted from the entropy before the split. The result is the Information Gain or decrease in entropy.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.09.29 PM.png" alt="Screenshot 2026-04-25 at 3.09.29 PM" style="zoom:50%;" />

### Entropy and Information Gain

Step 3:

Choose attribute with the largest **information gain as the decision node**, divide the dataset by its branches and repeat the same process for every branch.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.09.57 PM.png" alt="Screenshot 2026-04-25 at 3.09.57 PM" style="zoom:50%;" />

### Entropy and Information Gain

Step 4a:

Calculate the entropy of the target for each branch.

A branch that its entropy of target equals 0 is a **leaf node**.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.10.33 PM.png" alt="Screenshot 2026-04-25 at 3.10.33 PM" style="zoom:50%;" />

Step 4b:

A branch that its entropy of target is more than 0 needs further splitting.  
Calculate the information gain for non-leaf branches.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.11.11 PM.png" alt="Screenshot 2026-04-25 at 3.11.11 PM" style="zoom:50%;" />

#### Step 5:

The algorithm is run recursively on the non-leaf branches until all data is classified.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.11.49 PM.png" alt="Screenshot 2026-04-25 at 3.11.49 PM" style="zoom:50%;" />

## REGRESSION TREES

### Example

We begin with a simple example.

- We use the *Hitters* data set to predict a baseball player's (log) Salary based on **Years** (the number of years that he has played in the major leagues) and **Hits** (the number of hits that he made in the previous year).
- Salary is color-coded from low (blue, green) to high (yellow, red)

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.12.53 PM.png" alt="Screenshot 2026-04-25 at 3.12.53 PM" style="zoom:50%;" />

#### Example (cont'd)

- The top split assigns observations having  $\text{Years} < 4.5$  to the left branch. The predicted salary for these players is given by **the mean response value** for the players in the data set with  $\text{Years} < 4.5$ . For such players, the mean log salary is 5.107, and so we make a prediction of  $e^{5.107}$  thousands of dollars, i.e., \$165,174.
- Players with  $\text{Years} \geq 4.5$  are assigned to the right branch, and then that group is further subdivided by Hits. Overall, the tree stratifies or segments the players into three regions of **predictor space**:

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.13.13 PM.png" style="zoom:50%;" />

$$R_1 = \{X \mid \text{Years} < 4.5\}$$

$$R_2 = \{X \mid \text{Years} \geq 4.5, \text{Hits} < 117.5\}$$

$$R_3 = \{X \mid \text{Years} \geq 4.5, \text{Hits} \geq 117.5\}$$

The predicted salaries for these three groups are:

$$\$1,000 \times e^{5.107} = \$165,174$$

$$\$1,000 \times e^{5.999} = \$402,834$$

$$\$1,000 \times e^{6.740} = \$845,346$$

### Terminology for Trees

- In keeping with the *tree* analogy, the regions  $R_1$ ,  $R_2$ , and  $R_3$  are known as *terminal nodes*
- Decision trees are typically drawn *upside down*, in the sense that the *leaves* are at the bottom of the tree.
- The points along the tree where the predictor space is split are referred to as *internal nodes*
- Refer to the node segments of the trees that connect the nodes as *branches*.

### Tree-building Process

Roughly speaking, there are two steps for the process of building a regression tree.

1. We divide the predictor space — that is, the set of possible values for  $X_1, X_2, \dots, X_p$  — into  $J$  distinct and non-overlapping regions,  $R_1, R_2, \dots, R_J$ .
2. For every observation that falls into the region  $R_j$ , we make the same prediction, which is simply the mean of the response values for the training observations in  $R_j$ .

### Tree-building Process

- How do we construct the regions  $R_1, R_2, \dots, R_J$ ?
- In theory, the regions could have any shape. However, we choose to divide the predictor space into high-dimensional *rectangles*, or *boxes*, for simplicity and for ease of interpretation of the resulting predictive model.
- The goal is to find boxes  $R_1, R_2, \dots, R_J$  that minimize the RSS, given by

$$\sum_{j=1}^J \sum_{i \in R_j} (y_i - \hat{y}_{R_j})^2$$

where  $\hat{y}_{R_j}$  is the mean response for the training observations within the  $j$ th box.

### Tree-building Process

- Unfortunately, it is computationally infeasible to consider every possible partition of the feature space into  $J$  boxes.
- For this reason, we take a *top-down, greedy* approach that is known as *recursive binary splitting*.
- The approach is *top-down* because it begins at the top of the tree and then successively splits the predictor space; each split is indicated via two new branches further down on the tree.
- It is *greedy* because at each step of the tree-building process, the *best* split is made at that particular step, rather than looking ahead and picking a split that will lead to a better tree in some future step.

#### Recursive Binary Splitting

- To perform recursive binary splitting, we first select the predictor  $X_j$  and the cut-point  $s$  such that splitting the predictor space into the regions  $\{X|X_j < s\}$  and  $\{X|X_j \geq s\}$  leads to the **greatest** possible reduction in RSS.
- That is, we consider all predictors  $X_1, X_2, \dots, X_p$ , and **all possible** values of the cut-point  $s$  for each of the predictors, and then choose the predictor and cut-point such that the resulting tree has the lowest RSS.
- For any  $j$  and  $s$ , we define the pair of half-planes

$$R_1(j, s) = \{X|X_j < s\} \text{ and } R_2(j, s) = \{X|X_j \geq s\},$$

and we seek the value of  $j$  and  $s$  that minimize the equation

$$\sum_{i: x_i \in R_1(j, s)} (y_i - \hat{y}_{R_1})^2 + \sum_{i: x_i \in R_2(j, s)} (y_i - \hat{y}_{R_2})^2,$$

where  $\hat{y}_{R_1}$  is the mean response for the training observations in  $R_1(j, s)$ ,

And  $\hat{y}_{R_2}$  is the mean response for the training observations in  $R_2(j, s)$ .

### Tree-building Process

- Next, we repeat the process, looking for the best predictor and best cut-point in order to split the data further so as to minimize the RSS within each of the resulting regions.
- However, this time, instead of splitting the entire predictor space, we split one of the two previously identified regions. We now have three regions.
- Again, we look to split one of these three regions further, so as to minimize the RSS. The process continues until a stopping criterion is reached; for instance, we may continue until no region contains more than five observations.
- Once the regions  $R_1, R_2, \dots, R_J$  have been created, we predict the response for a given test observation using the mean of the training observations in the region to which that test observation belongs.

#### Example

- A five-region example of this approach is shown below.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.15.45 PM.png" alt="Screenshot 2026-04-25 at 3.15.45 PM" style="zoom:50%;" />

- Top Left: A partition of two-dimensional feature space that could not result from recursive binary splitting.
- Top Right: The output of recursive binary splitting on a two-dimensional example.



- Bottom Left: A tree corresponding to the partition in the top right panel.

- Bottom Right: A perspective plot of the prediction surface corresponding to that tree.

  <img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.16.31 PM.png" alt="Screenshot 2026-04-25 at 3.16.31 PM" style="zoom:50%;" />



#### Pruning a Tree

- The process described above may produce good predictions on the training set, but is likely to *overfit* the data, leading to poor test set performance. This is because the resulting tree might be too complex.
- A smaller tree with fewer splits (that is, fewer regions  $R_1, \dots, R_J$ ) might lead to lower variance and better interpretation at the cost of a little bias.
- One possible alternative to the process described above is to grow the tree only so long as the decrease in the RSS due to each split exceeds some (high) threshold.
- This strategy will result in smaller trees but is too *short-sighted*: a seemingly worthless split early on in the tree might be followed by a very good split — that is, a split that leads to a large reduction in RSS later on.
- A better strategy is to grow a very large tree  $T_0$ , and then prune it back to obtain a subtree.

How do we determine the best prune way to prune the tree?

- Intuitively, our goal is to select a subtree that leads to the lowest **test error** rate.
- *Cost complexity pruning* — also known as *weakest link pruning* — is used to do this
- Rather than considering every possible subtree, we consider a sequence of trees indexed by a nonnegative tuning parameter  $\alpha$ . For each value of  $\alpha$  there corresponds a subtree  $T \subset T_0$  such that

$$
\sum_{m=1}^{|T|} \sum_{i: x_i \in R_m} (y_i - \hat{y}_{R_m})^2 + \alpha|T|
$$

is as small as possible. Here  $|T|$  indicates the number of terminal nodes of the tree  $T$ ,  $R_m$  is the rectangle (i.e., the subset of predictor space) corresponding to the  $m$ th terminal node, and  $\hat{y}_{R_m}$  is the mean of the training observations in  $R_m$ .

#### Choosing the Best Subtree

- The tuning parameter  $\alpha$  controls a trade-off between the subtree's complexity and its fit to the training data.
- When  $\alpha = 0$ , then the subtree  $T$  will simply equal  $T_0$ . However, as  $\alpha$  increases, there is a price to pay for having a tree with many terminal nodes, and so the objective function will tend to be minimized for a smaller subtree.
- We select an optimal value  $\hat{\alpha}$  using cross-validation.
- We then return to the full data set and obtain the subtree corresponding to  $\hat{\alpha}$ .

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.18.42 PM.png" alt="Screenshot 2026-04-25 at 3.18.42 PM" style="zoom:50%;" />

### Baseball Example (cont'd)

- First, we randomly divided the data set in half, yielding 132 observations in the training set and 131 observations in the test set.
- We then built a large regression tree on the training data and varied  $\alpha$  to create subtrees with different numbers of terminal nodes.
- Finally, we performed six-fold cross-validation to estimate the cross-validated MSE of the trees as a function of  $\alpha$ .

### Baseball Example (cont'd)

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.19.28 PM.png" alt="Screenshot 2026-04-25 at 3.19.28 PM" style="zoom:50%;" />

Regression tree analysis for the Hitters data. The unpruned tree that results from top-down greedy splitting on the training data is shown.

#### Baseball Example (cont'd)

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.20.05 PM.png" style="zoom:50%;" />

The training, cross-validation, and test MSE are shown as a function of the number of terminal nodes in the pruned tree. Standard error bands are displayed. The minimum cross-validation error occurs at a tree size of three.

## CLASSIFICATION TREES

- A classification tree is very similar to a regression tree, except that it is used to predict a *qualitative response* rather than a quantitative one.
- For a classification tree, we predict that each observation belongs to the *most commonly occurring class* of training observations in the region to which it belongs.
- We are often interested not only in the class prediction corresponding to a particular terminal node region, but also in the *class proportions* among the training observations that fall into that region.
- Just as in the regression setting, we use recursive binary splitting to grow a classification tree.
- In the classification setting, RSS cannot be used as a criterion for making the binary splits

- A natural alternative to RSS is the *classification error rate*. This is simply the fraction of the training observations in that region that do not belong to the most common class:

$$E = 1 - \max_k(\hat{p}_{mk})$$

- Here  $\hat{p}_{mk}$  represents the proportion of training observations in the  $m$ th region that are from the  $k$ th class.
- However, classification error rate is not sufficiently sensitive for tree-growing, and in practice two other measures are preferable, i.e., *Gini Index* or *Entropy*.

- The Gini Index is defined by

$$G = \sum_{k=1}^K \hat{p}_{mk}(1 - \hat{p}_{mk})$$

a measure of *total variance across the  $K$  classes*. The Gini Index takes on a *small value* if all of the  $\hat{p}_{mk}$  are close to zero or one.

- For this reason, the Gini Index is referred to as a measure of node ***purity*** — a small value indicates that a node contains predominantly observations from a single class.

### Gini Index & Cross-Entropy

- An alternative to the Gini Index is *Cross-Entropy*, given by

$$D = - \sum_{k=1}^K \hat{p}_{mk} \log \hat{p}_{mk}$$

- Since  $0 \leq \hat{p}_{mk} \leq 1$ , it follows that  $-\hat{p}_{mk} \log \hat{p}_{mk} \geq 0$ .
- The entropy will take on a value near zero if the  $\hat{p}_{mk}$  are all near zero or near one. Therefore, the entropy will take on a small value if the  $m$ th node is pure.
- It turns out that the Gini Index and the Cross-Entropy are very similar numerically.
- When building a classification tree, either the Gini Index or the Entropy are typically used to evaluate the quality of a particular split, since these two approaches are sensitive to node **purity**.
- Any of these three approaches might be used when *pruning* the tree, but the classification error rate is preferable if prediction accuracy of the final pruned tree is the goal.

#### Example: Heart data set

- These data contain a binary outcome heart disease (HD) for 303 patients who presented with chest pain.
- An outcome value of *Yes* indicates the presence of heart disease based on an angiographic test, while *No* means no heart disease.
- There are 13 predictors including *Age*, *Sex*, *Chol* (a cholesterol measurement), and other heart and lung function measurements.
- Cross-validation results in a tree with six terminal nodes. See next figure.

#### Example: Heart data set (cont’d)

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.22.58 PM.png" style="zoom:50%;" />

The figure shows the **unpruned tree**. Some of the predictors, such as *Sex*, *Thal* (Thallium stress test), and *ChestPain*, are qualitative. For instance, the left-hand branch come from the first value of the *Thal* variable (normal), and the right-hand branch from the remaining values (fixed or reversible defects) of the *Thal* variable .

A surprising characteristic: some of the splits yield two terminal nodes that have the same predicted value. The split is performed because it leads to increased *node purity*. For instance, consider the split  $\text{RestECG} < 1$ . That is, all 9 of the observations corresponding to the right-hand leaf have a response value of *Yes*, whereas 7/11 of those corresponding to the left-hand leaf have a response value of *Yes*. **(certain or less certain)**

#### Example: Heart data set (cont'd)

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.23.38 PM.png" alt="Screenshot 2026-04-25 at 3.23.38 PM" style="zoom:50%;" />

Left: Cross-validation error, training, and test error, for different sizes of the pruned tree.

Right: The pruned tree corresponding to the minimal cross-validation error.

### Advantages and Disadvantages

- Trees are very easy to explain to people. In fact, they are even easier to explain than linear regression!
- Some people believe that decision trees more closely mirror human decision-making than do the regression and classification approaches.
- Trees can be displayed graphically and are easily interpreted even by a non-expert (especially if they are small).
- Trees can easily handle qualitative predictors without the need to create dummy variables.
- Unfortunately, trees generally do not have the same level of predictive accuracy as some of the other regression and classification approaches.

However, by aggregating many decision trees, the predictive performance of trees can be substantially improved. We introduce these concepts next.





# Tree-Based Methods (II)

### Issue of Decision Tree

- The simple decision trees for regression or classification discussed before suffer from *high variance*.
- This means that if we split the training data into two parts at random, and fit a decision tree to both halves, the results that we get could be quite different.
- In contrast, a procedure with low variance will yield similar results if applied repeatedly to distinct data sets; linear regression tends to have low variance, if the ratio of  $n$  to  $p$  is moderately large.
- To overcome the issue, we introduce ensemble methods.

### Ensemble Method

- An ensemble method is an approach that combines many simple “building ensemble block” models in order to obtain a single and potentially very powerful model.
- These simple building block models are sometimes known as weak learners, since they may lead to mediocre predictions on their own.
- We will now discuss bagging, random forests, and boosting. These are ensemble methods for which the simple building block is a regression or a classification tree.

### BAGGING

#### Bagging

- *Bootstrap aggregation*, or *bagging*, is a general-purpose procedure for reducing the variance of a statistical learning method.
- Recall that given a set of  $n$  independent observations  $Z_1, \dots, Z_n$ , each with variance  $\sigma^2$ , the variance of the mean  $\bar{Z}$  of the observations is given by

$$\text{Var}(\bar{Z}) = \frac{\sigma^2}{n}$$

- In other words, *averaging a set of observations reduces variance*.

#### Bootstrap aggregation

- Hence a natural way to reduce the variance and increase the test set accuracy of a statistical learning method is to take many training sets from the population, build a separate prediction model using each training set, and average the resulting predictions.
- Of course, we generally do not have access to multiple training sets. Instead, we can bootstrap, by taking repeated samples from the (single) training data set.

- In this approach we generate  $B$  different bootstrapped training data sets. We then train our method on each bootstrapped training set to get  $B$  different decision trees.
- Calculate  $\hat{f}^1(x), \hat{f}^2(x), \dots, \hat{f}^B(x)$ , the predictions at a point  $x$ , using  $B$  separate decision trees.
- Then average all the predictions to obtain a single low-variance statistical learning model, given by

$$\hat{f}_{\text{bag}}(x) = \frac{1}{B} \sum_{b=1}^B \hat{f}^{*b}(x)$$

This is called *bagging*.

### Regression vs. Classification

- For regression trees,
  - we simply construct  $B$  regression trees using  $B$  bootstrapped training sets, and average the resulting predictions. These trees are grown deep, and *are not pruned*. Hence each individual tree has high variance, but low bias. Averaging these  $B$  trees reduces the variance.
- For classification trees,
  - for each test observation, we record the class predicted by each of the  $B$  trees, and take a *majority vote*: the overall prediction is the most commonly occurring class among the  $B$  predictions.

### Out-of-Bag Error Estimation

- There is a very straightforward way to estimate the test error of a bagged model.
- With bagging, trees are repeatedly fit to bootstrapped **subsets** of the observations. On average, each bagged tree makes use of around two-thirds of the observations.
- The remaining one-third of the observations not used to fit a given bagged tree are referred to as the out-of-bag (OOB) observations.
- We can predict the response for the  $i$ th observation using each of the trees in which the  $i$ th observation was OOB. This will yield around  $B/3$  predictions for the  $i$ th observation, which we average.
- This estimate is equivalent to leave-one-out cross-validation error for bagging, if  $B$  is large.

#### Bagging the heart data

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.28.21 PM.png" style="zoom:50%;" />

- The test error rate (black and orange) is shown as a function of  $B$ , the number of trees constructed using bootstrapped training data sets.
- The dashed line indicates the test error resulting from a **single** classification **tree**.
- The green and blue traces show the OOB error, which in this case is considerably lower

Using a very large value of  $B$  will not lead to overfitting. In practice, we use a value of  $B$  sufficiently large that the error has settled down. Using  $B = 100$  is sufficient to achieve good performance in this example.

#### Variable Importance Measure

- For bagged *regression* trees, we record the total amount that the RSS is decreased due to splits over a given predictor, averaged over all  $B$  trees. A large value indicates an important predictor.
- Similarly, for bagged *classification* trees, we add up the total amount that the Gini Index is decreased by splits over a given predictor, averaged over all  $B$  trees.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.28.50 PM.png" style="zoom:50%;" />

### **RANDOM FORESTS**

#### Issue with Bagging

- As in bagging, we build a number of decision trees on bootstrapped training samples. Each of splits considers all predictors.
- Suppose that there is one very strong predictor in the data set, along with a number of other moderately strong predictors.
- Then in the collection of bagged trees, most or all trees will use this strong predictor in the top split (root node). Consequently, all of the bagged trees will look quite similar to each other.
- Hence the predictions from the bagged trees will be highly **correlated**. Unfortunately, averaging many highly correlated quantities does not lead to as large of a reduction in variance as averaging many uncorrelated quantities. This means that bagging will not lead to a substantial reduction in variance over a single tree in this setting.

#### Random Forests

- Random Forests provide an improvement over bagged trees by way of a small tweak that decorrelates the trees. This reduces the variance when we average the trees.
- Random Forests overcome this problem by forcing each split to consider only a subset of the predictors.
- But in Random Forests, when building these decision trees, each time a split in a tree is considered, a random selection of  $m$  predictors is chosen as split candidates from the full set of  $p$  predictors. The split is allowed to use only one of those  $m$  predictors.
- A **fresh** selection of  $m$  predictors is taken at each split, and typically we choose  $m \approx \sqrt{p}$  — that is, the number of predictors considered at each split is approximately equal to the square root of the total number of predictors (4 out of the 13 for the Heart data).

- On average  $(p - m)/p$  of the splits will not even consider the strong predictor, and so other predictors will have more of a chance. We can think of this process as decorrelating the trees, thereby making the average of the resulting trees less variable and hence more reliable.
- The main difference between bagging and random forests is the choice of predictor subset size  $m$ . For instance, if a random forest is built using  $m = p$ , then this amounts simply to bagging.
- Using a small value of  $m$  in building a random forest will typically be helpful when we have a large number of correlated predictors.

#### Example: gene expression data

- We applied random forests to a high-dimensional biological data set consisting of expression measurements of 4,718 genes measured on tissue samples from 349 patients.
- There are around 20,000 genes in humans, and individual genes have different levels of activity, or expression, in particular cells, tissues, and biological conditions.
- Each of the patient samples has a qualitative label with 15 different levels: either normal or one of 14 different types of cancer (response variable).
- We use random forests to predict cancer type based on the 500 genes that have the largest variance in the training set.
- We randomly divided the observations into a training and a test set, and applied random forests to the training set for three different values of  $m$ .

#### Example: gene expression data

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.30.00 PM.png" style="zoom:50%;" />

- Results from random forests for the 15-class gene expression data set with  $p = 500$  predictors.
- The test error is displayed as a function of the number of trees.

- Each colored line corresponds to a different value of  $m$ , the number of predictors available for splitting at each interior tree node.
- Random forests ( $m < p$ ) lead to a slight improvement over bagging ( $m = p$ ). A single classification tree has an error rate of 45.7%.

### BOOSTING

- Recall that bagging involves creating multiple copies of the original training data set using the bootstrap, fitting a separate decision tree to each copy, and then combining all of the trees in order to create a single predictive model.
- Notably, each tree is built on a bootstrap data set, independent of the other trees.
- Boosting works in a similar way, except that the trees are grown *sequentially*: each tree is grown using information from previously grown trees.
- Boosting does not involve bootstrap sampling; instead, each tree is fit on a modified version of the original data set.

#### Boosting for Regression Trees

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.30.29 PM-7156242.png" alt="Screenshot 2026-04-25 at 3.30.29 PM" style="zoom:50%;" />

#### The idea behind this procedure

- As  $b = 1$ , we fit a decision tree to the response  $Y$ .
- Start from  $b = 2$ , we fit a decision tree to the residuals from the model. That is, we fit a tree using the current residuals, rather than the outcome  $Y$ , as the response. We then add this new decision tree into the fitted function in order to update the residuals.
- Each of these trees can be rather small, with just a few terminal nodes, determined by the parameter  $d$  in the algorithm.
- By fitting small trees to the residuals, we slowly improve  $\hat{f}$  in areas where it does not perform well. The shrinkage parameter  $\lambda$  slows the process down even further, allowing more and different shaped trees to attack the residuals.

#### Tuning Parameters

- The number of trees  $B$ . Boosting can overfit if  $B$  is too large. We use cross-validation to select  $B$ .
- The shrinkage parameter  $\lambda$ , a small positive number. This controls the rate at which boosting learns. Typical values are 0.01 or 0.001, and the right choice can depend on the problem. Very small  $\lambda$  can require using a very large value of  $B$  to achieve good performance.
- The number of splits  $d$  in each tree, which controls the complexity of the boosted ensemble. Often  $d = 1$  works well, in which case each tree is a *stump*, consisting of a single split and resulting in an additive model. More generally  $d$  is the *interaction depth*, and controls the interaction order of the boosted model, since  $d$  splits can involve at most  $d$  variables.

#### Example: gene expression data (cont'd)

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.31.29 PM.png" style="zoom:50%;" />

- Results from performing boosting and random forests on the 15-class gene expression data set to predict *cancer* versus *normal*.
- The test error is displayed as a function of the number of trees.

- For the two boosted models,  $\lambda = 0.01$ . Depth-1 trees slightly outperform depth-2 trees, and both outperform the random forest, although the standard errors are around 0.02, making none of these differences significant.
- The test error rate for a single tree is 24%.

### Summary

- Decision trees are simple and interpretable models for regression and classification
- However, they are often not competitive with other methods in terms of prediction accuracy
- Bagging, random forests and boosting are good methods for improving the prediction accuracy of trees. They work by growing many trees on the training data and then combining the predictions of the resulting ensemble of trees.
- The latter two methods — random forests and boosting — are among the state-of-the-art methods for supervised learning. However, their results can be difficult to interpret.

# Resampling Methods

##### Outline

- Cross-Validation
- The Bootstrap

##### Resampling Methods

- Resampling methods are an indispensable tool in modern statistics.
- They involve repeatedly drawing samples from a training set and refitting a model of interest on each sample.
- Such an approach may allow us to obtain information that would not be available from fitting the model only once using the original training sample.
- Two of the most commonly used resampling methods are *cross-validation* and the *bootstrap*. For instance,
  - Cross-validation for : model assessment (MSE), model selection
  - Bootstrap for: confidence interval estimate

### CROSS-VALIDATION

#### Training Error vs. Test Error

- The test error is the average error that results from using a statistical learning method to predict the response on a new observation, one that was not used in training the method.

The test error can be easily calculated if a designated test set is available. Unfortunately, this is usually not the case.

- In contrast, the training error can be easily calculated by applying the statistical learning method to the observations used in its training.

But the training error rate often is quite different from the test error rate, and in particular the former can dramatically underestimate the latter.

### Training Error vs. Test Error

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.33.51 PM.png" style="zoom:50%;" />

### The Validation Set Approach

- Best solution: a large designated test set, but often not available.
- Hence, we consider a class of methods that **estimate the test error** by *holding out* a subset of the training observations from the fitting process. We randomly divide the available set of samples into two parts: a *training set* and a *validation* or *hold-out set*.
- The model is fit on the training set, and the fitted model is used to predict the responses for the observations in the *validation set* or *hold-out set*.
- The resulting validation-set error provides an estimate of the test error. This is typically assessed using *MSE* in the case of a quantitative response and *misclassification rate* in the case of a qualitative (discrete) response.

#### Example: Auto data

We randomly split the 392 observations into two sets, a training set containing 196 of the data points, and a validation set containing the remaining 196 observations.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.34.49 PM.png" alt="Screenshot 2026-04-25 at 3.34.49 PM" style="zoom:50%;" />

Left panel shows single split. Right panel shows multiple MSE curves, produced using ten different random splits of the observations into training and validation sets. There is **no consensus** among the curves as to which model results in the smallest validation set MSE.

#### Issues with Validation Set Approach

- The validation estimate of the test error can be highly variable, depending on precisely which observations are included in the training set and which observations are included in the validation set.
- In the validation approach, only a subset of the observations — those that are included in the training set rather than in the validation set — are used to fit the model.
- Since statistical methods tend to perform worse when trained on *fewer observations*. This suggests that the validation set error may tend to *overestimate* the test error for the model fit on the entire data set.

## Cross-Validation

Cross-validation, a refinement of the validation set approach, addresses these two issues.

- Leave-One-Out Cross-Validation (LOOCV)
- $k$ -Fold Cross-Validation

#### Leave-One-Out Cross-Validation

- LOOCV involves splitting the set of observations into two parts, leaves only a single observation  $(x_l, y_l)$  out for the validation set, and the remaining  $(n - 1)$  observations make up the training set.
- A prediction is made for the excluded single observation to approximate unbiased estimate for the test error.
- Repeating this approach  $n$  times until every observation was the validation set once and produces  $n$  squared errors.
- The LOOCV estimate for the test MSE is the average of these  $n$  test error estimates:

$$CV_{(n)} = \frac{1}{n} \sum_{i=1}^n MSE_i$$

where

$$MSE_i = (y_i - \hat{y}_i)^2$$

#### Leave-One-Out Cross-Validation

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.35.51 PM.png" style="zoom:50%;" />

A schematic display of LOOCV. A set of  $n$  data points is repeatedly split into a training set (shown in blue) containing all but one observation, and a validation set that contains only that single observation (shown in beige). The test error is then estimated by averaging the  $n$  resulting MSEs.

#### Advantages of LOOCV

- It has far less bias. we repeatedly fit the model using training sets that contain  $(n - 1)$  observations, almost as same as the entire data set. Consequently, the LOOCV approach tends not to overestimate the test error rate
- LOOCV will always yield the same results: there is no randomness in the training/validation set splits.
- LOOCV has the potential to be expensive to implement, since the model must be fit  $n$  times. This can be very time consuming if  $n$  is large.
- In the context of **least squares regression (only)** as it does not hold in general, a shortcut formula makes the cost of LOOCV the same as that of a single model fit.

$$CV_{(n)} = \frac{1}{n} \sum_{i=1}^n \left( \frac{y_i - \hat{y}_i}{1 - h_i} \right)^2$$

- where  $\hat{y}_i$  is the  $i$ th **fitted** value from the original least squares fit,  $h_i$  is diagonal elements of Hat Matrix, the variance of the fitted value.

## k-Fold Cross-Validation

- An alternative to LOOCV is  $k$ -fold CV.
- Estimates can be used to select best model, and to give an idea of the test error of the final chosen model.
- This approach involves randomly dividing the set of observations into  $k$  groups, or folds, of approximately equal size.
- We leave out part  $k$  as a validation set, fit the model to the remaining  $(K - 1)$  parts (combined as the training set), and then obtain predictions and MSE for the left-out  $k$ th part.

#### $k$ -Fold Cross-Validation

- This procedure is repeated  $k$  times; each time, a different group of observations is treated in turn for  $k = 1, 2, \dots, K$  as a validation set.
- This process results in  $k$  estimates of the test error,  $MSE_1, MSE_2, \dots, MSE_k$ . The  $k$ -fold CV estimate is computed by averaging these values,

$$CV_{(k)} = \frac{1}{k} \sum_{i=1}^k MSE_i$$

#### $k$ -Fold Cross-Validation

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.36.32 PM.png" alt="Screenshot 2026-04-25 at 3.36.32 PM" style="zoom:50%;" />

A schematic display of 5-fold CV. A set of  $n$  observations is randomly split into five non-overlapping groups. Each of these fifths acts as a validation set (shown in beige), and the remainder as a training set (shown in blue). The test error is estimated by averaging the five resulting MSE estimates.

- It is not hard to see that LOOCV is a special case of  $k$ -fold CV in which  $k$  is set to equal  $n$ .
- In practice, one typically performs  $k$ -fold CV using  $k = 5$  or  $k = 10$ . What is the advantage of using  $k = 5$  or  $k = 10$  rather than  $k = n$ ?
- Cross-validation is a very general approach that can be applied to almost any statistical learning method. Some statistical learning methods have computationally intensive fitting procedures, and so performing LOOCV may pose computational problems, especially if  $n$  is extremely large.
- In contrast, performing 10-fold CV requires fitting the learning procedure only ten times, which may be much more feasible.

#### Accuracy of the CV estimate

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.39.35 PM.png" style="zoom:50%;" />

When we examine real data, we do not know the true test MSE, so it is difficult to determine the accuracy of the cross-validation estimate. However, if we examine simulated data, then we can compute the *true* test MSE, and can thereby evaluate the accuracy of our cross-validation results.

#### Accuracy of the CV estimate

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.39.58 PM.png" style="zoom:50%;" />

The true test MSE is shown in blue, the LOOCV estimate is shown as a black dashed line, and the 10-fold CV estimate is shown in orange. In all three plots, the two cross-validation estimates are very similar. The crosses indicate the minimum of each of the MSE curves.

#### Two Goals of the CV estimate

##### Model assessment (MSE)

When we perform cross-validation, our goal might be to determine how well a given statistical learning procedure can be expected to perform on independent data; in this case, the actual estimate of the test MSE is of interest.

##### Model selection

But at other times we are interested only in the location of the minimum point in the estimated test MSE curve.

This is because we might be performing cross-validation on a number of statistical learning methods, or on a single method using different levels of flexibility, in order to identify the method that results in the lowest test error.

For this purpose, the location of the minimum point in the estimated test MSE curve is important, but the actual value of the estimated test MSE is not.

### Bias-Variance Trade-Off for k-Fold CV

- $k$ -fold CV gives more accurate estimates of the test error rate than does LOOCV due to a bias-variance trade-off.
- Empirically, using  $k = 5$  or  $10$  for  $k$ -fold cross-validation yields test error rate estimates that suffer **neither** from excessively high bias **nor** from very high variance.

From the perspective of bias reduction,

- LOOCV gives approximately **unbiased** estimates of the test error, since each training set contains  $(n-1)$  observations, which is almost as many as the number of observations in the full data set.
- $k$ -fold CV for, say,  $k = 5$  or  $k = 10$  will lead to an **intermediate level of bias**, since each training set contains approximately  $(k - 1)n/k$  observations — fewer than in the LOOCV approach.

- LOOCV has **higher variance** than does  $k$ -fold CV with  $k < n$ .

From the perspective of variance

- When we perform LOOCV, we are in effect averaging the outputs of  $n$  fitted models, each of which is trained on an **almost identical** set of observations; therefore, these outputs are highly (positively) **correlated** with each other.
- In contrast, when we perform  $k$ -fold CV with  $k < n$ , we are averaging the outputs of  $k$  fitted models that are somewhat **less correlated** with each other, since the overlap between the training sets in each model is smaller.
- Since the mean of many highly **correlated** quantities has higher variance than does the mean of many quantities that are not as highly correlated,
- Hence, the test error estimate resulting from LOOCV tends to have higher variance than does the test error estimate resulting from  $k$ -fold CV.

#### $k$ -Fold CV on Classification

In classification setting, we use the number of misclassified observations. For instance, the LOOCV error rate takes the form

$$CV_{(n)} = \frac{1}{n} \sum_{i=1}^n \text{Err}_i$$

where

$$\text{Err}_i = I(y_i \neq \hat{y}_i)$$

The  $k$ -fold CV error rate takes the form

$$CV_K = \sum_{k=1}^K \frac{n_k}{n} \text{Err}_k$$

where

$$\text{Err}_k = \sum_{i \in C_k} I(y_i \neq \hat{y}_i) / n_k$$

### THE BOOTSTRAP

- The bootstrap procedure is to obtain distinct data sets by repeatedly sampling observations from the original data set with replacement.
- Each of these “bootstrap data sets” is created by sampling with replacement and is the same size as our original dataset. As a result, some observations may appear more than once in a given bootstrap data set and some not at all.
- The bootstrap is a flexible and powerful statistical tool that can provide an estimate of the standard error of a coefficient, or a confidence interval for that coefficient.

#### Example

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.43.50 PM.png" style="zoom:50%;" />

A graphical illustration of the bootstrap approach on a small sample containing  $n = 3$  observations. Each bootstrap data set contains  $n$  observations, sampled with replacement from the original data set. Each bootstrap data set is used to obtain an estimate of  $\alpha$ .

#### Example

- We wish to determine the best investment allocation for an investment.
- Suppose that we wish to invest a fixed sum of money in two financial assets that yield returns of  $X$  and  $Y$ , respectively, where  $X$  and  $Y$  are random quantities. We will invest a fraction  $\alpha$  of our money in  $X$ , and will invest the remaining  $1 - \alpha$  in  $Y$ .
- Since there is variability associated with the returns on these two assets, we wish to choose  $\alpha$  to minimize the total risk, or variance, of our investment. In other words, we want to minimize  $\text{Var}(\alpha X + (1 - \alpha)Y)$ . The value that minimizes the risk is given by

$$\alpha = \frac{\sigma_Y^2 - \sigma_{XY}}{\sigma_X^2 + \sigma_Y^2 - 2\sigma_{XY}}$$

- where  $\sigma_X^2 = \text{Var}(X)$ ,  $\sigma_Y^2 = \text{Var}(Y)$ , and  $\sigma_{XY} = \text{Cov}(X, Y)$ .

#### Example: Simulation vs. Bootstrap

- For comparison, we use two methods to generate samples to estimate  $\alpha$ .
- We repeatedly **simulate** 100 paired observations of X and Y for 1000 times and estimate  $\alpha$  1,000 times. For these simulations, the parameters were set to  $\sigma_X^2 = 1$ ,  $\sigma_Y^2 = 1.25$ , and  $\sigma_{XY} = 0.5$ , and so we know that the true value of  $\alpha$  is 0.6 (in the original population).
- The mean over all 1,000 estimates for  $\alpha$  is

$$\bar{\alpha} = \frac{1}{1000} \sum_{r=1}^{1000} \hat{\alpha}_r = 0.5996.$$

- Very close to  $\alpha = 0.6$ , and the standard deviation of the estimates is

$$\sqrt{\frac{1}{1000 - 1} \sum_{r=1}^{1000} (\hat{\alpha}_r - \bar{\alpha})^2} = 0.083.$$

- Use the **bootstrap** approach to obtain 1000 new data sets from a single original data set.

#### Example

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.44.27 PM.png" style="zoom:50%;" />

**Left:** A histogram of the estimates of  $\alpha$  obtained by generating 1,000 simulated data sets from the true population. **Center:** A histogram of the estimates of  $\alpha$  obtained from 1,000 bootstrap samples from a single data set. **Right:** The estimates of  $\alpha$  displayed in the left and center panels are shown as boxplots. In each panel, the pink line indicates the true value of  $\alpha$ .

# Dimension Reduction (I)

## REVIEW CONCEPT

### Eigenvalues and Eigenvectors

Recall the characteristic equation

$$\Sigma \gamma = \lambda \gamma$$

$\lambda$  are eigenvalues,  $\gamma$  eigenvectors, and  $\Sigma$  is a *square* matrix. The eigenvalues can be found by solving

$$\det(\Sigma - \lambda I) = 0$$

where  $I$  is the identity matrix. Then the eigenvectors can be found by solving

$$(\Sigma - \lambda I)\gamma = 0$$

### Orthogonal and Orthonormal vectors

**Definition.** We say that 2 vectors are orthogonal if they are perpendicular to each other. i.e., the dot product of the two vectors is zero.

Example: the set of vectors is mutually orthogonal.  $\begin{pmatrix} 1 \\ 0 \\ -1 \end{pmatrix}, \begin{pmatrix} 1 \\ \sqrt{2} \\ 1 \end{pmatrix}, \begin{pmatrix} 1 \\ -\sqrt{2} \\ 1 \end{pmatrix}$

$$\begin{aligned}(1, 0, -1) \cdot (1, \sqrt{2}, 1) &= 0 \\ (1, 0, -1) \cdot (1, -\sqrt{2}, 1) &= 0 \\ (1, \sqrt{2}, 1) \cdot (1, -\sqrt{2}, 1) &= 0\end{aligned}$$

**Definition.** A set of vectors  $S$  is orthonormal if every vector in  $S$  has norm 1 (unit vector) and the set of vectors are mutually orthogonal.

Example: let

$$\begin{aligned}\vec{u}_1 &= \frac{\vec{v}_1}{|\vec{v}_1|} = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 0 \\ -1 \end{pmatrix} = \begin{pmatrix} 1/\sqrt{2} \\ 0 \\ -1/\sqrt{2} \end{pmatrix} \\ \vec{u}_2 &= \frac{\vec{v}_2}{|\vec{v}_2|} = \frac{1}{2} \begin{pmatrix} 1 \\ \sqrt{2} \\ 1 \end{pmatrix} = \begin{pmatrix} 1/2 \\ \sqrt{2}/2 \\ 1/2 \end{pmatrix} \\ \vec{u}_3 &= \frac{\vec{v}_3}{|\vec{v}_3|} = \frac{1}{2} \begin{pmatrix} 1 \\ -\sqrt{2} \\ 1 \end{pmatrix} = \begin{pmatrix} 1/2 \\ -\sqrt{2}/2 \\ 1/2 \end{pmatrix}\end{aligned}$$

The set of vectors  $\{\vec{u}_1, \vec{u}_2, \vec{u}_3\}$  is orthonormal.

## PRINCIPAL COMPONENTS ANALYSIS

#### Dimension Reduction

- Assume we have a dataset represented in an  $n \times D$  matrix  $X$  consisting of  $n$  data vectors  $x_i$  with dimensionality  $D$ .  $x_i$  is the  $i$ th row of  $X$ .
- Assume further that this dataset has intrinsic (inherent) dimensionality  $d$  (often  $d \ll D$ ).
- Dimensionality reduction techniques transform dataset  $X$  with dimensionality  $D$  into a new dataset  $Y$  with dimensionality  $d$ , while retaining the geometry of the data as much as possible.
- Principal component analysis (PCA) constructs a low-dimensional representation of the data that describes as much of the variance in the data as possible.

#### Principal Components Analysis 

The important properties of the new data set acquired by PCA:

- Principal components analysis transforms a set of observed variables into a new set of variables that are **uncorrelated** with one another.
- The transformed variables account for the variance of original variables in **sequentially decreasing proportions**.
- Each transformed variable in the new data set is called **PC score**. The first column PC score contains the greatest proportion of the total sample variance of the original data. The second column PC score accounts for a maximal proportion of the **remaining variance** subject to being uncorrelated with the first PC score. Subsequent components are defined similarly.
- The transformed variables (PC scores) are a linear combination of the original variables.

### Spectral Decomposition

A. L. Cauchy established the Spectral Decomposition in 1829.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.45.57 PM.png" style="zoom:50%;" />

Let  $A$  be a  $m \times m$  real symmetric matrix. Then there exists an orthogonal matrix  $P$  such that  $A = PDP^T$ , where  $D$  is a diagonal matrix.

### Spectral Decomposition

In multivariate analysis our data is a matrix. Suppose our data is matrix  $X$ . Suppose  $X_{m \times n}$  is mean centered, i.e.,  $X \rightarrow (X - \mu)$

and the variance-covariance matrix is  $\Sigma = (X - \mu)^T (X - \mu)$ . The variance-covariance matrix  $\Sigma$  is real and symmetric.

Using spectral decomposition, we can write  $\Sigma = PDP^T$ , where  $D$  is a diagonal matrix, i.e.,  $D = \text{diag}(\lambda_1, \lambda_2, \dots, \lambda_n)$  and  $\lambda_1, \dots, \lambda_n$  are eigenvalues of  $\Sigma$  and  $\lambda_1 \geq \lambda_2 \geq \dots \geq \lambda_n$ ,  $P$  is a matrix where each column is the corresponding orthonormal eigenvector  $u_1, \dots, u_n$  of  $\Sigma$ . The first eigenvector column is the **first principal component**, the second eigenvector column is the **second principal component**, and so on.

$$\Sigma = \underbrace{\begin{pmatrix} \uparrow & \uparrow & & \uparrow \\ v_1 & v_2 & \dots & v_n \\ \downarrow & \downarrow & & \downarrow \end{pmatrix}}_P \underbrace{\begin{pmatrix} \lambda_1 & & & 0 \\ & \lambda_2 & & \\ & & \ddots & \\ 0 & & & \lambda_n \end{pmatrix}}_{\Lambda} \underbrace{\begin{pmatrix} \leftarrow & v_1 & \rightarrow \\ \leftarrow & v_2 & \rightarrow \\ & \vdots & \\ \leftarrow & v_n & \rightarrow \end{pmatrix}}_{P^T}$$

### Spectral Decomposition

The new data (PC scores) via PC transformation is:

$$Y = (X - \mu) P$$

where,

$$E(Y_i) = 0$$

$$\text{Var}(Y_i) = \lambda_i$$

$$\text{Cov}(Y_i, Y_j) = 0 \text{ if } i \neq j$$

$$\text{Var}(Y_1) \geq \text{Var}(Y_2) \geq \dots \geq \text{Var}(Y_n)$$

$$\sum_{i=1}^n \text{Var}(Y_i) = \text{tr}(\Sigma) = \text{Total variation of Data} = \text{tr}(D)$$

$$\prod_{i=1}^n \text{Var}(Y_i) = |\Sigma|$$

### Singular Value Decomposition (SVD)

There are five mathematicians who made great contributions to establishment of the singular value decomposition and developing its theory, among others.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.46.58 PM.png" alt="Screenshot 2026-04-25 at 3.46.58 PM" style="zoom:50%;" />

The Singular Value Decomposition was originally developed by Eugenio Beltrami and Camille Jordan two mathematician in the mid to late 1800's.

Several other mathematicians took part in the final developments of the SVD including James Joseph Sylvester, Erhard Schmidt and Hermann Weyl who studied the SVD until the mid-1900's.

C.Eckart and G. Young prove low rank approximation of SVD (1936).

#### What is SVD?

Any real  $(m \times n)$  matrix  $X$ , where  $(n \leq m)$ , can be decomposed,

$$X = U \Lambda V^T$$

- $U$  is a  $(m \times n)$  column orthonormal matrix ( $U^T U = I$ ), containing the eigenvectors of the symmetric matrix  $XX^T$ .
- $\Lambda$  is a  $(n \times n)$  diagonal matrix, containing the **singular values** of matrix  $X$ . The number of non-zero diagonal elements of  $\Lambda$  corresponds to the rank of  $X$ .
- $V^T$  is a  $(n \times n)$  row orthonormal matrix ( $V^T V = I$ ), containing the eigenvectors of the symmetric matrix  $X^T X$ .

#### What is SVD?

Any real  $(m \times n)$  rectangular matrix  $X$ , where  $(n \leq m)$ , can be decomposed,

$$X = U \Lambda V^T$$

$$X_{m \times n} = \underbrace{\begin{pmatrix} \uparrow & \uparrow & & \uparrow \\ u_1 & u_2 & \cdots & u_n \\ \downarrow & \downarrow & & \downarrow \end{pmatrix}}_{U_{m \times n}} \underbrace{\begin{pmatrix} \sqrt{\lambda_1} & & & 0 \\ & \sqrt{\lambda_2} & & \\ & & \ddots & \\ 0 & & & \sqrt{\lambda_n} \end{pmatrix}}_{\Lambda_{n \times n}} \underbrace{\begin{pmatrix} \leftarrow & v_1 & \rightarrow \\ \leftarrow & v_2 & \rightarrow \\ & \vdots & \\ \leftarrow & v_n & \rightarrow \end{pmatrix}}_{V_{n \times n}^T}$$

Note that "singular values" of a matrix  $X$  are the positive **square roots of the eigenvalues** of the matrix product  $XX^T$  or  $X^T X$ , while "eigenvalues" of a matrix are simply the characteristic roots of the matrix itself,

Suppose  $X$  is a mean centered data matrix, Then  $X$  using SVD,

$$X = U\Lambda V^T$$

The new data (PC scores) can be calculated with

$$Y = XV = U\Lambda$$

Then the first columns of  $Y$  represents the first principal component score and so on.

- SVD Based PC is more Numerically Stable.
- If no. of variables is greater than no. of observations ( $m \gg n$ ), then SVD based PCA will give efficient result

#### Spectral Decomposition vs. SVD

Suppose  $X$  is a mean centered data matrix, Then  $X$  using SVD,

$$X = U\Lambda V^T$$

The variance-covariance matrix of  $X$  can be written as

$$\begin{aligned}\Sigma &= X^T X = (U\Lambda V^T)^T U\Lambda V^T \\ &= V\Lambda U^T U\Lambda V^T\end{aligned}$$

Because  $U$  is orthonormal eigenvector matrix, then  $U^T U = I$   
Hence,

$$\begin{aligned}\Sigma &= X^T X = (U\Lambda V^T)^T U\Lambda V^T \\ &= V\Lambda U^T U\Lambda V^T \\ &= V\Lambda \Lambda V^T \\ &= V D V^T = P D P^T\end{aligned}$$

where  $D = \Lambda^2$ ,  $V = P$

### Variance of New Data (PC Scores)

SVD based Principal Component Analysis (PCA) constructs a low dimensional representation of the data that describes as much of the variance in the data as possible.

The new data set (PC scores) can be written as

$$Y = XV = UA$$

where  $X$  is **mean centered (mean is removed)**. The variance-covariance of PC score variables  $Y$  is

$$\begin{aligned}\text{Var}(Y) &= E (XV)^T (XV) \\ &= V^T X^T X V \\ &= V^T \Sigma V \\ &= V^T P D P^T V \\ &= D = \text{diag}(\lambda_1, \lambda_2, \dots, \lambda_n)\end{aligned}$$

where  $V = P$ , and  $V^T P = I$ .

## Principal Components Analysis

Why do we need principal component technique?

#### 1. Dimension reduction

The general hope of principal components analysis is that the first few components will account for a substantial proportion of the variation in the original variables,  $x_1, \dots, x_q$ , and can, consequently, be used to provide a convenient **lower-dimensional summary of these variables** that might prove useful for a variety of reasons.

#### 2. As uncorrelated input to some other analysis, such as regression analysis

- There are **too many** explanatory variables relative to the number of observations.
- The explanatory variables are highly **correlated**.

### Find PCs

How are the principal components found?

The first PC is the **eigenvector of the sample covariance matrix**,  $\Sigma$ , corresponding to this matrix's largest eigenvalue.

The second PC is the eigenvector of the sample covariance matrix,  $\Sigma$ , corresponding to this matrix's second largest eigenvalue, and so on.

So on ...

### PC1 vs. PC2

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.48.31 PM.png" style="zoom:50%;" />

The figure shows that PC1 vs. PC2 principal components of some data points in two dimensions.

### Total Variance

The total variance of the  $q$  principal components will equal the total variance of the original variables so that

$$\sum_{i=1}^q \lambda_i = s_1^2 + s_2^2 + \cdots + s_q^2,$$

where  $S_i^2$  is the sample variance of  $x_i$ ,  $\lambda_i$  is the diagonal element of the sample covariance matrix  $\Sigma$ . We can write this more concisely as

$$\begin{aligned} \sum_{i=1}^q \text{Var}(Y_i) &= \sum_{i=1}^q \lambda_i = \text{tr}(\Sigma) \\ &= \text{Total variation of Data} = \text{tr}(D) \end{aligned}$$

### Account for Total Variance

Consequently, the  $j$ th principal component accounts for a proportion  $P_j$  of the total variation of the original data, where

$$P_j = \frac{\lambda_j}{\text{trace}(\Sigma)}$$

The first  $m$  principal components, where  $m < q$  account for a proportion  $P^{(m)}$  of the total variation in the original data, where

$$P^{(m)} = \frac{\sum_{j=1}^m \lambda_j}{\text{trace}(\Sigma)}$$

### Determine the Number of PCs

How many components are needed to provide an adequate summary of a given data set? The most common of the relatively ad hoc procedures that have been suggested.

- Retain just enough components to explain some specified large percentage of the total variation of the original variables. Values between 70% and 90% are usually suggested, although smaller values might be appropriate as  $q$  or  $n$ , the sample size, increases.
- Exclude those principal components whose eigenvalues are less than the average,  $\sum_{i=1}^q \lambda_i / q$ . Since  $\sum_{i=1}^q \lambda_i = \text{trace}(\Sigma)$ , the average eigenvalue is also the average variance of the original variables. This method then retains those components that account for more variance than the average for the observed variables

### Determine the Number of PCs

- Examination of the plot of the  $\lambda_i$  against  $i$ , the so-called scree diagram. The number of components selected is the value of  $i$  corresponding to an “elbow” in the curve, i.e., a change of slope from “steep” to “shallow”.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.51.40 PM.png" style="zoom:50%;" />

- A modification of the scree diagram is the log-eigenvalue diagram consisting of a plot of  $\log(\lambda_i)$  against  $i$ .

### Covariance vs. Correlation Matrix

Should principal components be extracted from the covariance or the correlation matrix?

One problem with principal components analysis is that it is not scale-invariant. Suppose the three variables in a multivariate data set are weight in **pounds**, height in **feet**, and age in **years**, but for some reason we would like our principal components expressed in **ounces**, **inches**, and **decades**. Intuitively two approaches seem feasible;

1. Multiply the variables by 16, 12, and  $1/10$ , respectively and then carry out a principal components analysis on the covariance matrix of the three variables.
2. Carry out a principal components analysis on the covariance matrix of the original variables and then multiply the elements of the relevant component by 16, 12, and  $1/10$ .

**Unfortunately, these two procedures do not generally lead to the same result.**

Principal components should only be extracted from the sample **covariance matrix, S**, when all the original variables have **roughly the same scale**. But this is rare in practice and consequently, in practice, principal components are extracted from the **correlation matrix** of the variables, **R**.

Extracting the components as the eigenvectors of **R** is equivalent to calculating the principal components from the original variables after each has been standardized to have **unit variance**. It should be noted, however, that there is rarely any simple correspondence between the components derived from **S** and those derived from **R**. And choosing to work with **R** rather than with **S** involves a definite but possibly arbitrary decision to make variables “**equally important**”.

## **PRINCIPAL COMPONENTS REGRESSION**

#### Principal Components Regression

- PCR dimension reduction methods work in two steps. First, the transformed predictors  $Z_1, Z_2, \dots, Z_M$  are obtained. Second, the model is fit using these  $M$  predictors with least squares.
- When performing PCR, we generally recommend standardizing each predictor prior to generating the principal components. This standardization ensures that all variables are on the same scale.
- In the absence of standardization, the high-variance variables will tend to play a larger role in the principal components obtained, and the scale on which the variables are measured will ultimately influence the final PCR model.

#### Principal Components Regression

In many situations we have a large number of inputs, often very correlated. The PCR method produces a small number of linear combinations  $Z_m$ ,  $m = 1, \dots, M$  of the original inputs  $X_j$ , and the  $Z_m$  are then used in place of the  $X_j$  as inputs in the regression. In this approach the linear combinations  $Z_m$  used are the principal component **scores** defined as

$$Z_m = \sum_{j=1}^p \phi_{jm} X_j$$

where  $\phi_m = [\phi_{1m}, \phi_{2m}, \dots, \phi_{pm}]^T$  is the  $m$ th eigenvector,  $m = 1, \dots, M$ .

### Principal Components Regression

and then regresses  $\mathbf{y}$  on  $z_1, z_2, \dots, z_M$  using least squares for some  $M \leq p$ . Since the  $z_m$  are orthogonal, this regression is just a sum of univariate regressions:

$$y_i = \theta_0 + \sum_{m=1}^M \theta_m z_{im} + \epsilon_i, \quad i = 1, \dots, n,$$

where  $\theta_0, \theta_1, \dots, \theta_M$  are the regression coefficients, which can be estimated by

$$\hat{\theta}_m = \langle \mathbf{z}_m, \mathbf{y} \rangle / \langle \mathbf{z}_m, \mathbf{z}_m \rangle$$

### Principal Components Regression

Since the  $z_m$  are each linear combinations of the original  $x_j$ , we can express the solution in terms of coefficients of the  $x_j$

$$\sum_{m=1}^M \theta_m z_{im} = \sum_{m=1}^M \theta_m \sum_{j=1}^p \phi_{jm} x_{ij} = \sum_{j=1}^p \sum_{m=1}^M \theta_m \phi_{jm} x_{ij} = \sum_{j=1}^p \beta_j x_{ij},$$

where

$$\beta_j = \sum_{m=1}^M \theta_m \phi_{jm}.$$

The term dimension reduction comes from the fact that this approach reduces the problem of estimating the  $(p+1)$  coefficients  $\beta_0, \beta_1, \dots, \beta_p$  to the simpler problem of estimating the  $(M+1)$  coefficients  $\theta_0, \theta_1, \dots, \theta_M$ , where  $M < p$ .

### PC Line vs. Least Squared Line

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.54.22 PM.png" style="zoom:50%;" />

# Dimension Reduction(II)

#### Outline

- Ridge Regression
- Lasso Regression
- Partial Least Squares

#### Shrinkage Methods

We can fit a model containing all  $p$  predictors using a technique that *constrains* or *regularizes* the coefficient estimates, or equivalently, that shrinks the coefficient estimates towards zero.

It may not be immediately obvious why such a constraint should improve the fit, but it turns out that shrinking the coefficient estimates can significantly reduce their variance.

The two best-known techniques for shrinking the regression coefficients towards zero are *ridge regression* and *the lasso*.

### RIDGE REGRESSION

#### Ridge regression

Recall that the least squares fitting procedure estimates  $\beta_0, \beta_1, \dots, \beta_p$  using the values that minimize

$$\text{RSS} = \sum_{i=1}^n \left( y_i - \beta_0 - \sum_{j=1}^p \beta_j x_{ij} \right)^2$$

Ridge regression is very similar to least squares, except that the coefficients are estimated by minimizing a slightly different quantity.

#### Ridge regression

Ridge regression shrinks the regression coefficients by imposing a penalty on their size in the objective function. In particular, the ridge regression coefficient estimates  $\hat{\beta}^{ridge}$  are the values that minimize a penalized residual sum of squares.

$$\begin{aligned}\hat{\beta}^{ridge} &= \arg \min_{\beta} \left\{ \sum_{i=1}^N \left( y_i - \beta_0 - \sum_{j=1}^P \beta_j x_{ij} \right)^2 + \lambda \sum_{j=1}^P \beta_j^2 \right\} \quad (1) \\ &= \arg \min_{\beta} \left\{ RSS + \lambda \sum_{j=1}^P \beta_j^2 \right\}\end{aligned}$$

Here  $\lambda \geq 0$  is a tuning parameter that controls the amount of shrinkage: the larger the value of  $\lambda$ , the greater the amount of shrinkage. The coefficients are shrunk toward zero (and each other). Selecting a good value for  $\lambda$  is critical and can be determined separately by cross-validation.

#### Ridge regression	

Equation (1) trades off two different criteria.

- As with least squares, ridge regression seeks coefficient estimates that fit the data well, by making the RSS small.
- However, the second term,  $\lambda \sum_j \beta_j^2$ , called a *shrinkage penalty*, is small when  $\beta_0, \beta_1, \dots, \beta_p$  are close to zero, and so it has the effect of the estimates of  $\beta_j$  towards zero.

The tuning parameter  $\lambda$  serves to control the relative impact of these two terms on the regression coefficient estimates.

- When  $\lambda = 0$ , the penalty term has no effect, and ridge regression will produce the least squares estimates.
- However, as  $\lambda \rightarrow \infty$ , the impact of the shrinkage penalty grows, and the ridge regression coefficient estimates will approach zero.

Unlike least squares, which generates only one set of coefficient estimates, ridge regression will produce a different set of coefficient estimates,  $\hat{\beta}^{ridge}$ , for each value of  $\lambda$ .

An equivalent way to write the ridge problem is

$$\hat{\beta}^{ridge} = \arg \min_{\beta} \sum_{i=1}^N \left( y_i - \beta_0 - \sum_{j=1}^P \beta_j x_{ij} \right)^2 \quad (2)$$

$$\text{subject to } \sum_{j=1}^P \beta_j^2 \leq t$$

which makes explicit the size constraint on the parameters.  
There is a one-to-one correspondence between the parameters  $\lambda$  in (1) and  $t$  in (2).

When applying Lagrange Multiplier to (2), we can obtain (1)

#### Ridge regression

When there are many correlated variables in a linear regression model, their coefficients can become poorly determined and exhibit high variance. A wildly large positive coefficient on one variable can be canceled by a similarly large negative coefficient on its correlated cousin. By imposing a size constraint  $t$  on the coefficients, this problem is alleviated.

In addition, notice that the intercept  $\beta_0$  has been left out of the penalty term. Penalization of the intercept would make the procedure depend on the origin chosen for  $Y$ ; that is, adding a constant  $C$  to each of the targets  $y_i$  would not simply result in a shift of the predictions by the same amount  $C$ .

#### Ridge regression

The ridge solutions are not equivariant under scaling of the inputs, and so one normally standardizes the inputs before solving (1).

The solution to (1) can be separated into **two parts**, after re-parametrization using centered inputs: each  $x_{ij}$  gets replaced By  $x_{ij} - \bar{x}_j$ .

We estimate  $\beta_0$  by  $\bar{y} = \frac{1}{N} \sum_1^N y_i$ . The remaining coefficients get estimated by a ridge regression without intercept, using the centered  $x_{ij}$ . Henceforth we assume that this centering has been done, so that the input matrix  $X$  has  $p$  (rather than  $p + 1$ ) columns.

#### Ridge regression

Equation (1) in matrix form:

$$L(\lambda) = (y - X\beta)^T (y - X\beta) + \lambda\beta^T \beta$$

The ridge regression solutions are

$$\hat{\beta}^{ridge} = (X^T X + \lambda I)^{-1} X^T y$$

where  $I$  is the  $p \times p$  identity matrix. Notice that with the choice of quadratic penalty  $\beta^T \beta$ , the ridge regression solution is again a linear function of  $y$ . The solution adds a positive constant to the diagonal of  $X^T X$  before inversion. This makes the problem non-singular, even if  $X^T X$  is not of full rank, and was the main motivation for ridge regression when it was first introduced in statistics (Hoerl and Kennard, 1970).

#### Ridge regression

The *singular value decomposition* (SVD) of the centered input matrix  $\mathbf{X}$  gives us some additional insight into the nature of ridge regression. The SVD of the  $N \times p$  matrix  $\mathbf{X}$  has the form

$$\mathbf{X} = \mathbf{U} \mathbf{D} \mathbf{V}^T$$

Here  $\mathbf{U}$  and  $\mathbf{V}$  are  $N \times p$  and  $p \times p$  orthogonal matrices, with the columns of  $\mathbf{U}$  spanning the column space of  $\mathbf{X}$ , and the columns of  $\mathbf{V}$  spanning the row space.  $\mathbf{D}$  is a  $p \times p$  diagonal matrix, with diagonal entries  $d_1 \geq d_2 \geq \dots \geq d_p \geq 0$  called the singular values of  $\mathbf{X}$ .

#### Ridge regression

Using the *singular value decomposition*, we can write the ridge solutions as

$$\begin{aligned}\mathbf{X}\hat{\beta}^{\text{ridge}} &= \mathbf{X}(\mathbf{X}^T \mathbf{X} + \lambda \mathbf{I})^{-1} \mathbf{X}^T \mathbf{y} \\ &= \mathbf{U} \mathbf{D} (\mathbf{D}^2 + \lambda \mathbf{I})^{-1} \mathbf{D} \mathbf{U}^T \mathbf{y} \\ &= \sum_{j=1}^p \mathbf{u}_j \frac{d_j^2}{d_j^2 + \lambda} \mathbf{u}_j^T \mathbf{y},\end{aligned}$$

where the  $\mathbf{u}_j$  are the columns of  $\mathbf{U}$ . Note that since  $\lambda \geq 0$ , we have  $d_j^2 / (d_j^2 + \lambda) \leq 1$ . Like linear regression, ridge regression computes the coordinates of  $\mathbf{y}$  with respect to the orthonormal basis  $\mathbf{U}$ . It then shrinks these coordinates by the factors  $d_j^2 / (d_j^2 + \lambda)$ . This means that a greater amount of shrinkage is applied to the coordinates of basis vectors with smaller  $d_j^2$ .

#### Ridge regression

This monotone decreasing function of  $\lambda$  is the *effective degrees of freedom* of the ridge regression fit.

$$\begin{aligned} \text{df}(\lambda) &= \text{tr}[\mathbf{X}(\mathbf{X}^T \mathbf{X} + \lambda \mathbf{I})^{-1} \mathbf{X}^T], \\ &= \text{tr}(\mathbf{H}_\lambda) \\ &= \sum_{j=1}^p \frac{d_j^2}{d_j^2 + \lambda}. \end{aligned}$$

Usually in a linear-regression fit with  $p$  variables, the degrees-of-freedom of the fit is  $p$ , the number of free parameters. The idea is that although all  $p$  coefficients in a ridge fit will be non-zero, they are fit in a restricted fashion controlled by  $\lambda$ . Note that  $\text{df}(\lambda) = p$  when  $\lambda = 0$  (no regularization) and  $\text{df}(\lambda) \rightarrow 0$  as  $\lambda \rightarrow \infty$ . Of course there is always an additional one degree of freedom for the intercept, which was removed *apriori*.

#### Example: Credit Data

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.57.57 PM.png" style="zoom:50%;" />

The panel displays each curve corresponds to the ridge regression coefficient estimate for one of the ten variables, as a function of  $\lambda$ .

As  $\lambda$  equals zero, the corresponding ridge coefficient estimates are the same as the usual least squares estimates. But as  $\lambda$  increases, the ridge coefficient estimates shrink towards zero.

#### Example: Credit Data

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.58.23 PM.png" style="zoom:50%;" />

The panel displays the same ridge coefficient estimates as a function of  $\|\hat{\beta}_\lambda^R\|_2 / \|\hat{\beta}\|_2$

As  $\lambda$  equals zero, the ratio equals zero, corresponding ridge coefficient estimates are the same as the usual least squares estimates. But as  $\lambda$  increases, the ratio reduced to zero, ridge coefficient estimates shrink towards zero.

#### Input Data Standardization

The standard least squares coefficient estimates discussed in early Chapter are scale equivariant: multiplying  $X_j$  by a constant  $c$  simply leads to a scale of the least squares coefficient estimates by a factor of  $1/c$ . In other words, regardless of how the  $j$ th predictor is scaled,  $X_j \hat{\beta}_j$  will remain the same.

In contrast, the ridge regression coefficient estimates can change substantially when multiplying a given predictor by a constant due to the sum of squared coefficients term in the ridge regression objective function.

Therefore, it is best to apply ridge regression after standardizing the predictors, using the formula

$$\tilde{x}_{ij} = \frac{x_{ij}}{\sqrt{\frac{1}{n} \sum_{i=1}^n (x_{ij} - \bar{x}_j)^2}}$$

As a result, the final model coefficients will not depend on the scale on which the predictors are measured.

#### Bias-Variance Trade-Off

*Why Does Ridge Regression Improve Over Least Squares?*

As  $\lambda$  increases, the flexibility of the ridge regression fit decreases, leading to decreased variance but increased bias.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 3.58.57 PM.png" style="zoom:50%;" />

Squared bias (black), variance (green), and test mean squared error (purple) for the ridge regression predictions on a simulated data set, as a function of  $\lambda$  and  $\|\hat{\beta}_\lambda^R\|_2 / \|\hat{\beta}\|_2$ . The horizontal dashed lines indicate the minimum possible MSE. The purple crosses indicate the ridge regression models for which the MSE is smallest.

#### *Why Does Ridge Regression Improve Over Least Squares?*

- In situations where the relationship between the response and the predictors is close to linear, the least squares estimates will have low bias but may have high variance.
- This means that a small change in the training data can cause a large change in the least squares coefficient estimates.
- In particular, when the number of variables  $p$  is almost as large as the number of observations  $n$  the least squares estimates will be extremely variable. And if  $p > n$ , then the least squares estimates do not even have a unique solution, whereas ridge regression can still perform well by trading off a small increase in bias for a large decrease in variance. Hence, ridge regression works best in situations where the least squares estimates have high variance.

### LASSO REGRESSION

**Issue:** Ridge regression will include all  $p$  predictors in the final model. The penalty  $\lambda \sum \beta_j^2$  in its objective function will shrink all of the coefficients towards zero, but it will not (exclude) set any of them exactly to zero (unless  $\lambda = \infty$ ).

It can create a challenge in model interpretation in settings in which the number of variables  $p$  is quite large.

The lasso is an alternative to ridge regression that overcomes this disadvantage. The lasso coefficients minimize the objective function:

$$\begin{aligned}\hat{\beta}^{lasso} &= \arg \min_{\beta} \left\{ \sum_{i=1}^N \left( y_i - \beta_0 - \sum_{j=1}^P \beta_j x_{ij} \right)^2 + \lambda \sum_{j=1}^P |\beta_j| \right\} \\ &= \arg \min_{\beta} \left\{ RSS + \lambda \sum_{j=1}^P |\beta_j| \right\}\end{aligned}\quad (3)$$

#### Lasso Regression

It is also equivalent to the following Lagrangian form of optimization problem.

$$\hat{\beta}^{lasso} = \arg \min_{\beta} \sum_{i=1}^N \left( y_i - \beta_0 - \sum_{j=1}^P \beta_j x_{ij} \right)^2 \quad (4)$$

subject to  $\sum_{j=1}^P |\beta_j| \leq t$

Just as in ridge regression, we can re-parameterize the constant  $\beta_0$  by standardizing the predictors; the solution for  $\hat{\beta}_0$  is  $\bar{Y}$ , and thereafter we fit a model without an intercept.

Note the similarity to the ridge regression equation (1) and (2): the  $L_2$  ridge penalty  $\sum_1^P \beta_j^2$  is replaced by the  $L_1$  lasso penalty  $\sum_1^P |\beta_j|$ . This latter constraint makes the solutions nonlinear in the  $y_i$ , and there is no closed form expression as in ridge regression.

#### Lasso Regression

- As with ridge regression, the lasso shrinks the coefficient estimates towards zero. However, in the case of the lasso, the  $\ell_1$  penalty has the effect of forcing some of the coefficient estimates to be exactly equal to zero when the tuning parameter  $\lambda$  is sufficiently large. In contrast, ridge regression will always include all of the variables in the model.
- As a result, models generated from the lasso are generally much easier to interpret than those produced by ridge regression. We say that the lasso yields sparse models — that is, sparse models that involve only a subset of the variables.

#### Example: Credit data

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.00.15 PM.png" style="zoom:50%;" />

The plot shows applying the lasso to the Credit data set.

When  $\lambda = 0$ , then the lasso simply gives the least squares fit, and when  $\lambda$  becomes sufficiently large, the lasso gives the null model in which all coefficient estimates equal zero.

#### Example: Credit data

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.00.57 PM.png" style="zoom:50%;" />

This shows the lasso (left) and ridge regression (right). The solid blue areas are the constraint regions,  $|\beta_1|+|\beta_2| \leq t$  and  $\beta_1^2 + \beta_2^2 \leq t$ , while the red ellipses are the contours of the RSS.

The lasso constraint has corners at each of the axes, and so the ellipse will often intersect the constraint region at an axis. When this occurs, one of the coefficients will equal zero.

#### Lasso vs. Ridge

*Which method leads to better prediction accuracy?*

The lasso has a major advantage over ridge regression, in that it produces simpler and more interpretable models that involve only a subset of the predictors. Some the coefficients will equal zero. However, the example illustrates that **neither** ridge regression **nor** the lasso will universally dominate the other.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.02.01 PM.png" style="zoom:50%;" />

Left: Plots of squared bias (black), variance (green), and test MSE (purple) for the lasso on a simulated data set. Right: Comparison of squared bias, variance, and test MSE between lasso (solid) and ridge (dotted).

#### Elastic-net Model

Partly for this reason as well as for computational tractability, Zou and Hastie (2005) introduced the *elastic-net* penalty

$$\lambda \sum_{j=1}^p (\alpha \beta_j^2 + (1 - \alpha) |\beta_j|), \quad (6)$$

a different compromise between ridge and lasso. The elastic-net selects variables like the lasso, and shrinks together the coefficients of correlated predictors like ridge. It also has considerable computational advantages over the  $L_q$  penalties.

## PARTIAL LEAST SQUARES

### Issue with PC Regression

The PCR approach involves identifying linear combinations, or directions, that best represent the predictors  $X_1, \dots, X_p$ . These directions are identified in an *unsupervised* way, since the response  $Y$  is not used to help determine the principal component directions. That is, *the response does not supervise the identification of the principal components*.

Consequently, PCR suffers from a drawback: there is *no guarantee* that the directions that *best explain the predictors* will also be the best directions to use for predicting the *response*.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.02.48 PM.png" style="zoom:50%;" />

The graph shows the advertising data, the first PLS direction (solid line) and first PCR direction (dotted line).

## Partial Least Squares

1. Standardize each  $\mathbf{x}_j$  to have mean zero and variance one. Set  $\hat{\mathbf{y}}^{(0)} = \bar{y}\mathbf{1}$ , and  $\mathbf{x}_j^{(0)} = \mathbf{x}_j$ ,  $j = 1, \dots, p$ .
2. For  $m = 1, 2, \dots, p$ 
  - (a)  $\mathbf{z}_m = \sum_{j=1}^p \hat{\varphi}_{mj} \mathbf{x}_j^{(m-1)}$ , where  $\hat{\varphi}_{mj} = \langle \mathbf{x}_j^{(m-1)}, \mathbf{y} \rangle$ .
  - (b)  $\hat{\theta}_m = \langle \mathbf{z}_m, \mathbf{y} \rangle / \langle \mathbf{z}_m, \mathbf{z}_m \rangle$ .
  - (c)  $\hat{\mathbf{y}}^{(m)} = \hat{\mathbf{y}}^{(m-1)} + \hat{\theta}_m \mathbf{z}_m$ .
  - (d) Orthogonalize each  $\mathbf{x}_j^{(m-1)}$  with respect to  $\mathbf{z}_m$ :  $\mathbf{x}_j^{(m)} = \mathbf{x}_j^{(m-1)} - [\langle \mathbf{z}_m, \mathbf{x}_j^{(m-1)} \rangle / \langle \mathbf{z}_m, \mathbf{z}_m \rangle] \mathbf{z}_m$ ,  $j = 1, 2, \dots, p$ .
3. Output the sequence of fitted vectors  $\{\hat{\mathbf{y}}^{(m)}\}_1^p$ . Since the  $\{\mathbf{z}_\ell\}_1^m$  are linear in the original  $\mathbf{x}_j$ , so is  $\hat{\mathbf{y}}^{(m)} = \mathbf{X}\hat{\beta}^{\text{pls}}(m)$ . These linear coefficients can be recovered from the sequence of PLS transformations.

## Partial Least Squares

- This technique also constructs a set of linear combinations of the inputs for regression, but unlike principal components regression it uses  $y$  (in addition to  $\mathbf{X}$ ) for this construction.
- Like principal component regression, partial least squares (PLS) is not scale invariant, so we assume that each  $x_j$  is standardized to have mean 0 and variance 1.
- In the construction of the derived input  $z_m$ , the inputs are weighted by the strength of their univariate effect on  $y$ .
- The outcome  $y$  is regressed on  $z_m$  giving coefficient  $\hat{\theta}_m$ .
- Since it uses the response  $y$  to construct its directions, its solution path is a nonlinear function of  $y$ . The partial least squares seeks directions that have high variance and high correlation with the response, in contrast to principal components regression which is only on high variance.

### Partial Least Squares

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.03.30 PM.png" style="zoom:50%;" />

- The tuning parameters for ridge and lasso vary over a *continuous* range, while PLS and PCR take just two *discrete* steps to the least squares solution, they all finally converges to least squares.
- PLS and PCR show similar behavior to ridge, roughly track the ridge path, although are discrete and more extreme. The behavior of the lasso is intermediate to the other methods.
- Ridge regression shrinks all directions, but shrinks low-variance directions more. Principal components regression leaves  $M$  high-variance directions alone, and discards the rest. Partial least squares also tends to shrink the low-variance directions, but can actually inflate some of the higher variance directions.

#### Summary and Comparison

$$\hat{\beta}(\lambda) = \operatorname{argmin}_{\beta} [R(\beta) + \lambda J(\beta)],$$

where

$$R(\beta) = \sum_{i=1}^N L(y_i, \beta_0 + \sum_{j=1}^p x_{ij}\beta_j),$$

where  $L$  is the loss function and  $J$  is the penalty function. The following are sufficient conditions for the solution  $\beta(\lambda)$

1.  $R$  is quadratic or piecewise-quadratic as a function of  $\beta$ .
2.  $J$  is piecewise linear in  $\beta$ .

A full study is given in Frank and Friedman (1993). These authors conclude that for minimizing prediction error, ridge regression is generally preferable to principal components regression and partial least squares. However the improvement over the latter two methods was only slight. The behavior of the lasso is intermediate to the other methods.



# Support Vector Machines

#### Outline

- Maximal Margin Classifier
- Support Vector Classifiers
- Support Vector Machines

#### A New Approach for Classification

- Support vector machine (SVM), an approach for classification, was developed in the computer science community in the 1990s and has grown in popularity since then.
- The support vector machine is a generalization of two simple intuitive classifiers:
  - maximal margin classifier
  - support vector classifier
- People often loosely refer to the maximal margin classifier, the support vector classifier, and the support vector machine as “support vector machines”.

### MAXIMAL MARGIN CLASSIFIER

#### What is a Hyperplane?

In a  $p$ -dimensional space, a **hyperplane** is a flat *affine* subspace of dimension  $p-1$ . For instance,

- In two dimensions, a hyperplane is a flat one-dimensional subspace — a line.
- In three dimensions, a hyperplane is a flat two-dimensional subspace — that is, a plane.
- In  $p > 3$  dimensions, it can be hard to visualize a hyperplane, but the notion of a  $(p-1)$ -dimensional flat subspace still applies.

The word *affine* indicates that the subspace need not pass through the origin.

#### What is a Hyperplane?

The mathematical definition of a *hyperplane* is quite simple. In two dimensions, a *hyperplane* is defined by the equation

$$\beta_0 + \beta_1 X_1 + \beta_2 X_2 = 0 \quad (1)$$

where  $\beta_0$ ,  $\beta_1$ , and  $\beta_2$  are parameters. Any  $X = (X_1, X_2)^T$  for which equation (1) holds is a point on the hyperplane. Note that the equation (1) is simply the equation of a line.

If extended to the  $p$ -dimensional setting:

$$\beta_0 + \beta_1 X_1 + \beta_2 X_2 + \cdots + \beta_p X_p = 0 \quad (2)$$

defines a  $p$ -dimensional *hyperplane*. Any point  $X = (X_1, X_2, \dots, X_p)^T$  in  $p$ -dimensional space (i.e., a vector of length  $p$ ) satisfies equation (2), then  $X$  lies on the hyperplane.

#### A Separating Hyperplane

Now, suppose that  $X$  does not satisfy the equation, but rather,

$$\beta_0 + \beta_1 X_1 + \beta_2 X_2 + \cdots + \beta_p X_p > 0.$$

Then this tells us that  $X$  lies to one side of the hyperplane. On the other hand, if

$$\beta_0 + \beta_1 X_1 + \beta_2 X_2 + \cdots + \beta_p X_p < 0,$$

then  $X$  lies on the other side of the hyperplane. So, we can think of the hyperplane as dividing  $p$ -dimensional space into two halves.

One can easily determine on which side of the hyperplane a point lies by simply calculating the sign of the left-hand side of equation (2).

#### Classification with a Hyperplane

Suppose that we have an  $n \times p$  data matrix  $X$  that consists of  $n$  training observations in  $p$ -dimensional space,

$$x_1 = \begin{pmatrix} x_{11} \\ \vdots \\ x_{1p} \end{pmatrix}, \dots, x_n = \begin{pmatrix} x_{n1} \\ \vdots \\ x_{np} \end{pmatrix}$$

and that these observations fall into two classes—that is,  $y_1, \dots, y_n \in \{-1, 1\}$  where  $-1$  represents one class and  $1$  the other class. We also have a test observation, a  $p$ -vector of observed features  $x^* = (x_1^* \dots x_p^*)^T$ .

Our goal is to develop a classifier with a *separating hyperplane* based on the training data that will correctly classify the test observation using its feature measurements.

#### Classification with a Hyperplane

Suppose that it is possible to construct a hyperplane that separates training observations perfectly according to their class labels.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.05.31 PM.png" style="zoom:50%;" />

Label the observations from the blue class as  $y_i = 1$  and those from the purple class as  $y_i = -1$ . Then a separating hyperplane has the property that

$$\beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \cdots + \beta_p x_{ip} > 0 \text{ if } y_i = 1,$$

$$\beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \cdots + \beta_p x_{ip} < 0 \text{ if } y_i = -1.$$

#### Classification with a Hyperplane

Equivalently, a separating hyperplane has the property that

$$y_i(\beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \dots + \beta_p x_{ip}) > 0$$

for all  $i = 1, \dots, n$ .

If a separating hyperplane exists, i.e.,  $\beta_0, \beta_1, \dots, \beta_p$  can be determined, then we can use it to construct a very natural classifier.

#### Classification with a Hyperplane

A test observation is assigned a class depending on which side of the hyperplane it is located.

The right-hand panel of Figure 1 shows an example of such a classifier.

If a separating hyperplane, i.e.,  $\beta_0, \beta_1, \dots, \beta_p$ , can be determined, then we classify the test observation  $x^*$  based on the sign of

$$f(x^*) = \beta_0 + \beta_1 x_1^* + \beta_2 x_2^* + \dots + \beta_p x_p^*$$

If  $f(x^*)$  is positive, then we assign the test observation to class 1, and if  $f(x^*)$  is negative, then we assign it to class  $-1$ .

We can also make use of the **magnitude** of  $f(x^*)$ . If  $f(x^*)$  is far from zero, then this means that  $x^*$  lies far from the hyperplane, and so we can be **confident** about our class assignment for  $x^*$ .

On the other hand, if  $f(x^*)$  is close to zero, then  $x^*$  is located near the hyperplane, and so we are less certain about the class assignment for  $x^*$ .

### Maximal Margin Classifier

In general, if our data can be perfectly separated using a hyperplane, then there will in fact exist an infinite number of such hyperplanes. We must have a reasonable way to decide which of the infinite possible separating hyperplanes to use.

A natural choice is the ***maximal margin hyperplane*** (also known as optimal separating hyperplane), which is the separating hyperplane that is **farthest** from the training observations.

That is, we can compute the (perpendicular) distance from each training observation to a given separating hyperplane; the smallest such distance is the minimal distance from the observations to the hyperplane and is known as the **margin**.

#### Maximal Margin Classifier

The maximal margin hyperplane is the separating hyperplane for which the **margin is largest** — that is, it is the hyperplane that has the **farthest minimum distance** to the training observations.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.08.16 PM.png" style="zoom:50%;" />

The maximal margin hyperplane is shown as a solid line. The margin is the distance from the solid line to either of the dashed lines. The two blue points and the purple point that lie on the dashed lines are the **support vectors**.

## Maximal Margin Classifier

- The maximal margin hyperplane represents the **mid-line** of the **widest** “slab” that we can insert between the two classes. This is known as the *maximal margin classifier*.
- Three training observations are equidistant from the maximal margin hyperplane and lie along the dashed lines indicating the width of the margin. These three observations are known as **support vectors** in  $p$ -dimensional space.
- They “support” the maximal margin hyperplane in the sense that if these points were moved slightly then the maximal margin hyperplane would move as well.
- The maximal margin hyperplane depends **directly on the support vectors**, but **not on the other observations**: a movement to any of the other observations would not affect the separating hyperplane.
- The fact that the maximal margin hyperplane depends **directly on only a small subset** of the observations is an important property.

#### Maximal Margin Classifier

Construct the maximal margin hyperplane based on a set of  $n$  training observations  $x_1, \dots, x_n \in \mathbb{R}^p$  and associated class labels  $y_1, \dots, y_n \in \{-1, 1\}$ .

Briefly, the maximal margin hyperplane is the solution to the optimization problem

$$\underset{\beta_0, \beta_1, \dots, \beta_p, M}{\text{maximize}} \quad M \quad (9.9)$$

$$\text{subject to} \quad \sum_{j=1}^p \beta_j^2 = 1, \quad (9.10)$$

$$y_i(\beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \dots + \beta_p x_{ip}) \geq M \quad \forall i = 1, \dots, n. \quad (9.11)$$

The constraint in (9.11)

$$y_i(\beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \dots + \beta_p x_{ip}) \geq M \quad \forall i = 1, \dots, n$$

guarantees that each observation will be on the correct side of the hyperplane, with some cushion, provided that  $M$  is positive.

#### Maximal Margin Classifier

Briefly, the maximal margin hyperplane is the solution to the optimization problem

$$\underset{\beta_0, \beta_1, \dots, \beta_p, M}{\text{maximize}} \quad M \quad (9.9)$$

$$\text{subject to} \quad \sum_{j=1}^p \beta_j^2 = 1, \quad (9.10)$$

$$y_i(\beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \dots + \beta_p x_{ip}) \geq M \quad \forall i = 1, \dots, n. \quad (9.11)$$

The constraint in (9.10)

$$\sum_{j=1}^p \beta_j^2 = 1,$$

guarantees that there is unique solution, as well, the perpendicular distance from the  $i$ th observation to the hyperplane is given by

$$y_i(\beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \dots + \beta_p x_{ip}).$$

#### Maximal Margin Classifier

- Therefore, the constraints (9.10) and (9.11) ensure that each observation is on the correct side of the hyperplane and at least a distance  $M$  from the hyperplane.
- Hence,  $M$  represents the margin of our hyperplane, and the optimization problem chooses  $\beta_0, \beta_1, \dots, \beta_p$  to maximize  $M$ .
- Although the maximal margin classifier is often successful, it can also lead to **overfitting** when  $p$  is large due to sensitivity to individual observations

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.09.42 PM.png" style="zoom:50%;" />

Right: An additional blue observation has been added, leading to a dramatic shift in the maximal margin hyperplane shown as a solid line.

### SUPPORT VECTOR CLASSIFIERS

#### Issue with Non-separable Case

Maximal margin classifier unfortunately cannot be applied to most data sets, since it requires that the classes be separable by a linear boundary.

In many cases no separating hyperplane exists, and so there is no maximal margin classifier. In this case, the optimization problem (9.9)–(9.11) has no solution with  $M > 0$ .

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.10.07 PM.png" style="zoom:50%;" />

For example, there are two classes of observations, shown in blue and in purple. In this case, the two classes are **not separable** by a hyperplane, and so the maximal margin classifier cannot be used.

#### Support Vector Classifier

In this case, we might be willing to consider a classifier based on a hyperplane that *does not perfectly* separate the two classes, in the interest of

- greater robustness to individual observations, and
- better classification of most of the training observations.

That is, it could be worthwhile to misclassify a few training observations to do a better job in classifying the remaining observations.

Developing a hyperplane that *almost* separates the classes is to use a so-called **soft margin**.

The generalization of the maximal margin classifier to the **non-separable** case is known as the *support vector classifier*.

#### Support Vector Classifier

The *support vector classifier*, sometimes called a *soft margin classifier*, allows some observations to be on the incorrect side of the margin, or even the incorrect side of the hyperplane. (The margin is *soft* because it can be violated by some of the training observations.)

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.11.20 PM.png" alt="Screenshot 2026-04-25 at 4.11.20 PM" style="zoom:50%;" />

#### Support Vector Classifier

The hyperplane is chosen to correctly separate **most** of the training observations into the two classes, but may misclassify a few observations. It is the solution to the optimization problem

$$\underset{\beta_0, \beta_1, \dots, \beta_p, \epsilon_1, \dots, \epsilon_n, M}{\text{maximize}} \quad M \quad (9.12)$$

$$\text{subject to} \quad \sum_{j=1}^p \beta_j^2 = 1, \quad (9.13)$$

$$y_i(\beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \dots + \beta_p x_{ip}) \geq M(1 - \epsilon_i), \quad (9.14)$$

$$\epsilon_i \geq 0, \quad \sum_{i=1}^n \epsilon_i \leq C, \quad (9.15)$$

where  $C$  is a nonnegative tuning parameter.  $M$  is the width of the margin. In (9.14),  $\epsilon_1, \dots, \epsilon_n$  are *slack variables* indicating the distance from the margin that individual observations are on the wrong side of the margin or the hyperplane.

#### Parameters

The slack variable  $\epsilon_i$  tells us where the  $i$ th observation is located, relative to the hyperplane and relative to the margin.

- If  $\epsilon_i = 0$  then the  $i$ th observation is on the correct side of the margin.
- If  $\epsilon_i > 0$  then the  $i$ th observation is on the wrong side of the margin.
- If  $\epsilon_i > 1$  then it is on the wrong side of the hyperplane.

In (9.15),  $C$  bounds the sum of the  $\epsilon_i$ 's, and so it determines the number and severity of the violations to the margin (and to the hyperplane) that we will tolerate.

- If  $C = 0$  then there is no budget for violations to the margin, and it must be the case that  $\epsilon_1 = \dots = \epsilon_n = 0$ , in which case (9.12)–(9.15) simply amounts to the maximal margin hyperplane (**only if** the two classes are separable).
- For  $C > 0$  no more than  $C$  observations can be on the wrong side of the hyperplane ( $\epsilon_i > 1$ ).
- As  $C$  increases, the margin will widen; as  $C$  decreases, the margin narrows.

#### Support Vectors

Only observations that either lie on the margin or that violate the margin will affect the hyperplane. Observations that lie directly on the margin, or on the wrong side of the margin for their class, are known as **support vectors**.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.19.18 PM.png" style="zoom:50%;" />

A support vector classifier was fit using **four** different values of the tuning parameter  $C$ .

When  $C$  is large, more support vectors, the margin will be large. (top-left)

As  $C$  decreases, less support vectors, the margin narrows. (bottom-right)

#### Bias-Variance Trade-off

In practice,  $C$  is treated as a tuning parameter that is generally chosen via  $k$ -fold cross-validation.

$C$  controls the bias-variance trade-off.

When  $C$  is small, we seek narrow margins that are rarely violated; this amounts to a classifier that is highly fit to the data, which may have **low bias but high variance**.

When  $C$  is larger, the margin is wider, and we allow more violations to it; this amounts to fitting the data less hard and obtaining a classifier that is potentially **more biased but may have lower variance**.

Once we have solved (9.12)–(9.15), we classify the test observation based on the sign of

$$f(x^*) = \beta_0 + \beta_1 x_1^* + \beta_2 x_2^* + \dots + \beta_p x_p^*$$

## SUPPORT VECTOR MACHINES

### Non-Linear Decision Boundaries

The limitation of maximal margin classifier and support vector classifier is that they can only classify the data with *linear* class boundary.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.20.32 PM.png" style="zoom:50%;" />

To accommodate non-linear class boundaries, we discuss a general mechanism for converting a linear classifier into one that produces non-linear decision boundaries.

### Non-Linear Decision Boundaries

- With an analogous situation, how do we make linear regression to fit a nonlinear relationship between the predictors and the outcome?
- We enlarge the feature space using functions of the predictors, such as quadratic and cubic terms, polynomial terms, to address this non-linearity.
- In the case of the support vector classifier, we could address the problem of possibly non-linear boundaries between classes **in a similar way**, by enlarging the feature space using quadratic, cubic, and even higher-order polynomial functions of the predictors.
- For instance, we could fit a support vector classifier using  $2p$  features

$$X_1, X_1^2, X_2, X_2^2, \dots, X_p, X_p^2.$$

### Non-Linear Decision Boundaries

Then (9.12)–(9.15) would become

$$\begin{aligned} & \underset{\beta_0, \beta_{11}, \beta_{12}, \dots, \beta_{p1}, \beta_{p2}, \epsilon_1, \dots, \epsilon_n, M}{\text{maximize}} & M & (9.16) \\ & \text{subject to } y_i \left( \beta_0 + \sum_{j=1}^p \beta_{j1} x_{ij} + \sum_{j=1}^p \beta_{j2} x_{ij}^2 \right) \geq M(1 - \epsilon_i), \\ & \sum_{i=1}^n \epsilon_i \leq C, \quad \epsilon_i \geq 0, \quad \sum_{j=1}^p \sum_{k=1}^2 \beta_{jk}^2 = 1. \end{aligned}$$

In the enlarged feature space, the decision boundary that results from (9.16) is in fact linear. But in the **original feature space**, the decision boundary is of the form of a quadratic polynomial, and its solutions are generally non-linear.

### Support Vector Machine

The support vector machine (SVM) is an extension of the support vector classifier that results from enlarging the feature space in a specific way, **using kernels**.

**Kernel approach** is simply an efficient computational approach for enlarging our feature space to accommodate a non-linear boundary between the classes.

Skipping the technical details of how the support vector classifier is computed, briefly, the **solution** to the support vector classifier problem (9.12)–(9.15) involves **only the inner products** of the observations.

For instance, the inner product of two observations  $x_i, x_{i'}$  is given by

$$\langle x_i, x_{i'} \rangle = \sum_{j=1}^p x_{ij} x_{i'j}.$$

### With Inner Product

- The linear *support vector classifier* can be represented as

$$f(x) = \beta_0 + \sum_{i=1}^n \alpha_i \langle x, x_i \rangle$$

where there are  $n$  parameters  $\alpha_i$ ,  $i = 1, \dots, n$ , one per training observation.

- To estimate the parameters  $\alpha_1, \dots, \alpha_n$  and  $\beta_0$ , all we need are the  $\binom{n}{2} = n(n-1)/2$  inner products  $\langle x_i, x_{i'} \rangle$  between all pairs of training observations.
- However, it turns out that  $\alpha_i$  is nonzero only for the **support vectors** in the solution — that is, if a training observation is not a support vector, then its  $\alpha_i$  equals zero.

#### With Kernel Function

A generalization of the inner product of the form

$$K(x_i, x_{i'})$$

where  $K$  is a function that is referred to as a kernel. Then support vector classifier can be represented as

$$f(x) = \beta_0 + \sum_{i \in \mathcal{S}} \alpha_i K(x, x_i).$$

When the kernel function takes the form

$$K(x_i, x_{i'}) = \sum_{j=1}^p x_{ij} x_{i'j},$$

$f(x)$  is a linear support vector classifier.

### Support Vector Machine

$$f(x) = \beta_0 + \sum_{i \in \mathcal{S}} \alpha_i K(x, x_i).$$

When the kernel function takes the form

$$K(x_i, x_{i'}) = \left(1 + \sum_{j=1}^p x_{ij} x_{i'j}\right)^d$$

known as a polynomial kernel of degree  $d$ , where  $d$  is a positive integer and  $d > 1$  for non-linear. Then the resulting classifier  $f(x)$  is known as a **support vector machine**. Another popular choice is the radial kernel, which takes the form

$$K(x_i, x_{i'}) = \exp\left(-\gamma \sum_{j=1}^p (x_{ij} - x_{i'j})^2\right).$$

where  $\gamma$  is a positive constant.

### Radial Kernel Behavior

How does the radial kernel actually work?

If a given test observation  $x^* = (x_1^*, \dots, x_p^*)^T$  is far from a training observation  $x_i$  in terms of Euclidean distance, then  $\sum_{j=1}^p (x_j^* - x_{ij})^2$  will be large, and so  $K(x^*, x_i) = \exp(-\gamma \sum_{j=1}^p (x_j^* - x_{ij})^2)$  will be tiny. This means that  $x_i$  will play virtually no role in  $f(x^*)$ .

In other words, training observations that are far from  $x^*$  will play essentially no role in the predicted class label for  $x^*$ . This means that the radial kernel has very *local* behavior, in the sense that **only nearby** training observations have an effect on the class label of a test observation.

### Advantage of Kernel

What is the advantage of using a **kernel** rather than simply enlarging the feature space using functions of the original features, as in (9.16)?

The greatest advantage is computational, and it amounts to the fact that using kernels, one needs only compute  $K(x_i, x_{i'})$  for all  $\binom{n}{2} = n(n-1)/2$  distinct pairs  $i, i'$ .

This can be done without explicitly working in the enlarged feature space. This is important because in many applications of SVMs, the enlarged feature space is so large that computations are intractable.

#### Example

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.39.53 PM.png" style="zoom:50%;" />

Left: An SVM with a polynomial kernel of degree 3 is applied to the non-linear data.

Right: An SVM with a radial kernel is applied.

In this example, either kernel is capable of capturing the decision boundary.

#### Application to the Heart Disease Data

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.50.20 PM.png" style="zoom:50%;" />

ROC curves for the Heart data **training set**.

Left: The support vector classifier and LDA are compared.

Right: The support vector classifier is compared to an SVM using a radial basis kernel. Using  $\gamma = 10^{-1}$  appears to give an almost perfect ROC curve.

#### Application to the Heart Disease Data

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.50.39 PM.png" style="zoom:50%;" />

ROC curves for the **test set** of the Heart data.

Left: The support vector classifier and LDA are compared.

Right: The support vector classifier is compared to an SVM using a radial basis kernel. Using  $\gamma = 10^{-1}$  produces the worst estimates on the test data.

### SVMs with More than Two Classes

SVM is for classification in the two-class setting.

Though a number of proposals for extending SVMs to the  $K$ -class case have been made, the two most popular are the

- one-versus-one
- one-versus-all approaches

### One-Versus-One Classification

Suppose that we would like to perform classification using SVMs, and there are  $K > 2$  classes. A *one-versus-one* or *all-pairs* approach constructs  $\binom{K}{2}$  SVMs, each of which compares a pair of classes.

For example, one such SVM might compare the  $k$ th class, coded as  $+1$ , to the  $k'$ th class, coded as  $-1$ .

We classify a test observation using each of the  $\binom{K}{2}$  classifiers, and we tally the number of times that the test observation is assigned to each of the  $K$  classes.

The final classification is performed by assigning the test observation to the class to which it was most frequently assigned in these pairwise classifications.

#### One-Versus-All Classification

The one-versus-all approach (also referred to as one-versus-rest) is an alternative procedure for applying SVMs in the case of  $K > 2$  classes. We fit  $K$  SVMs, each time comparing one of the  $K$  classes to the remaining  $K - 1$  classes.

Let  $\beta_{0k}, \beta_{1k}, \dots, \beta_{pk}$  denote the parameters that result from fitting an SVM comparing the  $k$ th class (coded as  $+1$ ) to the others (coded as  $-1$ ).

Let  $x^*$  denote a test observation.

We assign the observation to the class for which

$$\beta_{0k} + \beta_{1k}x_1^* + \beta_{2k}x_2^* + \dots + \beta_{pk}x_p^*$$

is **largest**, as this amounts to a high level of confidence that the test observation belongs to the  $k$ th class rather than to any of the other classes.

# Artificial Neural Network(II)

#### Neural Network Applications

Neural Network is one of the most important tools in predictive analytics and is the cornerstone of deep learning.

- Forecast, meteorology, road network traffic...
- Classification (image, video, etc.)
- Clustering
- Pattern recognition, computer vision...
- Large-scale Language inference, generative AI, ChatGPT
- Autonomous driving
- Facial recognition...

What is the working mechanism that enables Neural Networks to implement those tasks?

## A Single Neuron

- A single neuron is the basic **operator** in a Neural Network.
- The structure of a single neuron is schematically as follows:

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.52.15 PM.png" style="zoom:50%;" />

Activation functions  $f(\sum \omega x)$ :

- Sigmoid function
- Hyperbolic tangent sigmoid
- ReLU function
- Softmax function

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.53.01 PM.png" style="zoom:50%;" />

A typical architecture of Neural Networks consist of neurons, layers, and connections :

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.53.27 PM.png" style="zoom:50%;" />

A neural network takes an input vector of  $p$  variables  $X = (X_1, X_2, \dots, X_p)$  and builds a nonlinear function  $f(X)$  to predict the response  $Y$ . Figure above shows a simple **feed-forward neural network** for modeling a quantitative response using  $p = 4$  predictors. In the terminology of neural networks, the four features  $X_1, \dots, X_4$  make up the units in the **input layer**. The arrows indicate that each of the inputs from the input layer feeds into each of the  $K$  hidden input layer units.

### Single Layer Neural Networks

The mathematical form of a typical neural network model can be written as

$$\begin{aligned} f(X) &= \beta_0 + \sum_{k=1}^K \beta_k h_k(X) \\ &= \beta_0 + \sum_{k=1}^K \beta_k g(w_{k0} + \sum_{j=1}^p w_{kj} X_j). \end{aligned}$$

The model builds in two steps for feed-forward computation:

1. the **K activations**  $A_k$ ,  $k = 1, \dots, K$ , in the **hidden layer** are computed as functions of the input features  $X_1, X_2, \dots, X_p$ ,

$$A_k = h_k(X) = g(w_{k0} + \sum_{j=1}^p w_{kj} X_j)$$

where  $g(z)$  is a nonlinear activation function that is specified in advance. Each  $A_k$  can be seen as a different transformation of the original function features.

2. These **K activations** from the hidden layer then feed into the **output layer**, resulting in

$$f(X) = \beta_0 + \sum_{k=1}^K \beta_k A_k,$$

#### Parameters and Activation Function

All the parameters  $\beta_0, \beta_1, \dots, \beta_K$  and  $w_{k0}, w_{k1}, \dots, w_{kp}$  need to be estimated from data, the process of parameter estimation is called network training.

In the early instances of neural networks, the *sigmoid activation function* was favored, which is the same function used in logistic regression

$$g(z) = \frac{e^z}{1 + e^z} = \frac{1}{1 + e^{-z}}$$

The preferred choice in modern neural networks is the *ReLU (rectified linear unit) activation function*, which takes the form

$$g(z) = (z)_+ = \begin{cases} 0 & \text{if } z < 0 \\ z & \text{otherwise} \end{cases}$$

A ReLU activation can be computed and stored more efficiently than a sigmoid activation.

#### Example for feed-forward computation

The name ***neural network*** originally derived from thinking of these hidden units as analogous to **neurons in the brain** — values of the activations  $A_k$  close to one are *firing*, while those close to zero are *silent* (using the sigmoid activation function).

The nonlinearity in the activation function  $g(\cdot)$  is essential and allows the model to capture complex nonlinearities and interaction effects.

Consider a very simple example with  $p = 2$  input variables  $X = (X_1, X_2)$ , and  $K = 2$  hidden units with  $g(z) = z^2$ . We specify the other parameters as

$$\begin{aligned}\beta_0 &= 0, & \beta_1 &= \frac{1}{4}, & \beta_2 &= -\frac{1}{4}, \\ w_{10} &= 0, & w_{11} &= 1, & w_{12} &= 1, \\ w_{20} &= 0, & w_{21} &= 1, & w_{22} &= -1.\end{aligned}$$

#### Example for feed-forward computation

1. We get activations:

$$\begin{aligned}h_1(X) &= (0 + X_1 + X_2)^2, \\h_2(X) &= (0 + X_1 - X_2)^2.\end{aligned}$$

2. We get the model output:

$$\begin{aligned}f(X) &= 0 + \frac{1}{4} \cdot (0 + X_1 + X_2)^2 - \frac{1}{4} \cdot (0 + X_1 - X_2)^2 \\&= \frac{1}{4} [(X_1 + X_2)^2 - (X_1 - X_2)^2] \\&= X_1 X_2.\end{aligned}$$

Hence, the sum of two nonlinear transformations of linear functions can give us an interaction!

#### Objective Function

Fitting a neural network requires estimating the unknown parameters in neural network model  $\beta_0, \beta_1, \dots, \beta_K$  and  $w_{k0}, w_{k1}, \dots, w_{kp}$

$$\begin{aligned} f(X) &= \beta_0 + \sum_{k=1}^K \beta_k h_k(X) \\ &= \beta_0 + \sum_{k=1}^K \beta_k g(w_{k0} + \sum_{j=1}^p w_{kj} X_j) \end{aligned}$$

For a **quantitative response** (regression), typically **squared-error loss** is used as the objective function, so that the parameters are chosen to minimize

$$L(\theta | X) = \sum_{i=1}^n (y_i - f_\theta(x_i))^2$$

For a **qualitative response** (classification), typically multinomial log-likelihood is used as the objective function

$$L(\theta | X) = - \sum_{i=1}^n \sum_{m=1}^M y_{im} \log(f_m(x_i))$$

#### Multilayer Neural Networks

In theory a single hidden layer with a large number of units has the ability to approximate most functions.

However, the learning task of discovering a good solution is made much easier with multiple layers each of modest size.

Modern neural networks typically have more than one hidden layer, and often many units per layer.

#### **Example:**

A large dense neural network was built for the famous and publicly available ***MNIST*** handwritten digit dataset. Figure shows examples of these digits.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.55.07 PM.png" style="zoom:50%;" />

The goal is to build a model to classify the images into their correct digit class 0–9.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.55.24 PM.png" style="zoom:50%;" />

### MNIST Data Set	

Every image has  $p = 28 \times 28 = 784$  pixels, each of which is an eight-bit number (0–255) which represents how dark that pixel is.

These pixels are stored in the **input vector**  $X$ . The output is the class label, represented by a vector  $Y = (Y_0, Y_1, \dots, Y_9)$  of 10 dummy variables, with a **one** (“1”) in the position corresponding to the label, and zeros elsewhere, known as *one-hot encoding*.

There are 60,000 training images, and 10,000 test images.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.56.31 PM.png" alt="Screenshot 2026-04-25 at 4.56.31 PM" style="zoom:50%;" />

### Multilayer Neural Networks

A multilayer network architecture works well for solving the digit classification task. The input layer has  $p = 784$  units, two hidden layers  $L_1$  (256 units) and  $L_2$  (128 units). It has **ten** output variables. The loss function used for training the network is tailored for the multiclass classification task. This network has 235,146 parameters (referred to as weights).

The notation  $W_1$  represents the entire matrix of weights that feed from the input layer to the first hidden layer  $L_1$ . This matrix will have  $785 \times 256 = 200,960$  elements;

Each element  $A_k^{(1)}$  feeds to the second hidden layer  $L_2$  via the matrix of weights  $W_2$  of dimension  $257 \times 128 = 32,896$ .

The matrix  $B$  stores all  $129 \times 10 = 1,290$  of these weights.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.57.13 PM.png" style="zoom:50%;" />

### Multilayer Neural Networks

The first hidden layer is as

$$\begin{aligned} A_k^{(1)} &= h_k^{(1)}(X) \\ &= g(w_{k0}^{(1)} + \sum_{j=1}^p w_{kj}^{(1)} X_j) \end{aligned}$$

for  $k = 1, \dots, K_1 (=256)$ . The second hidden layer treats the activations  $A_k^{(1)}$  of the first hidden layer as inputs and computes new activations

$$\begin{aligned} A_\ell^{(2)} &= h_\ell^{(2)}(X) \\ &= g(w_{\ell 0}^{(2)} + \sum_{k=1}^{K_1} w_{\ell k}^{(2)} A_k^{(1)}) \end{aligned}$$

for  $\ell = 1, \dots, K_2 (=128)$ .

Thus, through **a chain of transformations**, the network is able to build up fairly complex transformations of  $X$  that ultimately feed into the output layer as features.

The **superscript** notation indicates to which layer the activations and weights (coefficients) belong.

#### Multilayer Neural Networks

We now get to the **output** layer, where we now have 10 responses

$$\begin{aligned} Z_m &= \beta_{m0} + \sum_{\ell=1}^{K_2} \beta_{m\ell} h_{\ell}^{(2)}(X) \\ &= \beta_{m0} + \sum_{\ell=1}^{K_2} \beta_{m\ell} A_{\ell}^{(2)}, \end{aligned}$$

for  $m = 0, 1, \dots, 9$ . However, we would like our estimates to represent class probabilities  $f_m(X) = \Pr(Y = m | X)$  which is **softmax** function.

$$f_m(X) = \Pr(Y = m | X) = \frac{e^{Z_m}}{\sum_{\ell=0}^9 e^{Z_{\ell}}},$$

for  $m = 0, 1, \dots, 9$ . Even though the goal is to build a classifier, the model actually estimates a **probability** for each of the 10 classes. The classifier then assigns the image to the class with the highest probability. To train this network, we look for coefficient estimates that minimize the negative multinomial log-likelihood known as the *cross-entropy*.

$$- \sum_{i=1}^n \sum_{m=0}^9 y_{im} \log(f_m(x_i))$$

#### Training Neural Network

- Any neural network must be trained with big data before it has the capacity to implement specific tasks.
- The essence of training neural networks is to find **optimal weight matrices** such that the neural networks can generate the output as close as possible to the target values. This is analogy to model estimation process for a regression model. It is also called **learning process**.
- The capacity of neural networks lies in the way it is trained with big data.
  - Supervised learning
  - Unsupervised learning
- Its capacity also depends on the data set used in training.
  - Traffic data
  - Image data
  - Language data
  - ...

### Training Neural Network

Given observations  $(x_i, y_i)$ ,  $i = 1, \dots, n$ , we could fit the model by solving a nonlinear least squares problem

$$\underset{\{w_k\}_1^K, \beta}{\text{minimize}} \frac{1}{2} \sum_{i=1}^n (y_i - f(x_i))^2,$$

where

$$f(x_i) = \beta_0 + \sum_{k=1}^K \beta_k g\left(w_{k0} + \sum_{j=1}^p w_{kj} x_{ij}\right)$$

We can rewrite the objective function as

$$R(\theta) = \frac{1}{2} \sum_{i=1}^n (y_i - f_\theta(x_i))^2,$$

### Example of Nonconvex Solutions

Because of the **nested** arrangement of the parameters and the symmetry of the hidden units, the problem is **nonconvex** in the parameters, and hence there are multiple solutions.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 4.59.41 PM.png" style="zoom:50%;" />

As an example, the figure shows a simple nonconvex function of a single variable  $\theta$ ; there are two solutions: one is a local minimum at  $\theta = -0.46$ , and the other is a global minimum at  $\theta = 1.02$ . In general, we can hope to end up at a (good) local minimum.

#### Two Step Operations

Neural Networks training is implemented via two-step operations:

- Feed forward propagation performs two tasks:
  1. feed data to neural network, through the network computation, to generate output.
  2. calculate the **discrepancy** between the output and the target value, i.e., the total error.

The goal of training is to minimize the discrepancy between the model output and the target value (observed value).

- Backward propagation performs two tasks:
  1. calculate gradient
  2. adjust the weight matrix

#### Gradient Descent Approach

In the 2<sup>nd</sup> step backward propagation, the solution can be found using **gradient descent** approach. The idea of gradient descent is very simple.

1. Start with a guess  $\theta^0$  for all the parameters in  $\theta$ , and set  $t = 0$ .
2. Iterate until the objective function fails to decrease:
  - (a) Find a vector  $\delta$  that reflects a small change in  $\theta$ , such that  $\theta_{t+1} = \theta_t + \delta$  reduces the objective; i.e., such that  $R(\theta_{t+1}) < R(\theta_t)$ .
  - (b) Set  $t \leftarrow t + 1$ .

#### Backpropagation

The gradient of  $R(\theta)$ , evaluated at some current value  $\theta = \theta^m$ , is the vector of the first-order partial derivatives at that point:

$$\nabla R(\theta^m) = \frac{\partial R(\theta)}{\partial \theta} \bigg|_{\theta=\theta^m}$$

This gives the direction in  $\theta$ -space in which  $R(\theta)$  *increases* most rapidly. **The idea of gradient descent** is to move  $\theta$  a little in the **opposite** direction (since we wish to go downhill), hence, the  $\theta$  is updated by the following formula:

$$\theta^{m+1} \leftarrow \theta^m - \rho \nabla R(\theta^m).$$

where  $\rho$  is the learning rate. This step will decrease the objective  $R(\theta)$ ; i.e.,  $R(\theta^{m+1}) \leq R(\theta^m)$  with a small enough value of the learning rate. If the gradient vector is zero, then we may have arrived at a minimum of the objective.

### Backpropagation

To get gradient for neural network model, we apply the **chain rule of differentiation** to the objective function

$$R_i(\theta) = \frac{1}{2} \left( y_i - \beta_0 - \sum_{k=1}^K \beta_k g(w_{k0} + \sum_{j=1}^p w_{kj} x_{ij}) \right)^2$$

First, we take the derivative with respect to  $\beta_k$ :

$$\begin{aligned} \frac{\partial R_i(\theta)}{\partial \beta_k} &= \frac{\partial R_i(\theta)}{\partial f_\theta(x_i)} \cdot \frac{\partial f_\theta(x_i)}{\partial \beta_k} \\ &= -(y_i - f_\theta(x_i)) \cdot g(z_{ik}). \end{aligned}$$

Then, we take the derivative with respect to  $w_{kj}$ :

$$\begin{aligned} \frac{\partial R_i(\theta)}{\partial w_{kj}} &= \frac{\partial R_i(\theta)}{\partial f_\theta(x_i)} \cdot \frac{\partial f_\theta(x_i)}{\partial g(z_{ik})} \cdot \frac{\partial g(z_{ik})}{\partial z_{ik}} \cdot \frac{\partial z_{ik}}{\partial w_{kj}} \\ &= -(y_i - f_\theta(x_i)) \cdot \beta_k \cdot g'(z_{ik}) \cdot x_{ij}. \end{aligned}$$

Where  $z_{ik} = w_{k0} + \sum_{j=1}^p w_{kj} x_{ij}$ . The act of differentiation assigns a fraction of the residual to each of the parameters via the chain rule — a process known as **backpropagation** in the neural network literature, i.e., redistribute total errors.

#### STEP BY STEP EXAMPLE

#### Feed Forward Propagation

From **input layer to hidden layer**:

$$X_j = \sum_{i=1}^{n_i} \omega_{ij} I_i \quad (1)$$

$$Y_j = f(X_j) = \frac{1}{1 + e^{-X_j}} \quad (2)$$

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.03.30 PM.png" style="zoom:50%;" />

From **hidden layer to output layer**:

$$X_k = \sum_{j=1}^{n_j} \omega_{jk} Y_j \quad (3)$$

$$Y_k = f(X_k) = \frac{1}{1 + e^{-X_k}} \quad (4)$$

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.03.44 PM.png" style="zoom:50%;" />

#### Feed Forward Propagation (cont'd)

- Our goal is to match the neural network output to the target values as close as possible.
- **Measure the discrepancy** between the output from the neural network model and the target values as follows:

$$E = \frac{1}{2} \sum_k (Y_k - O_k)^2 \quad (5)$$

- How can we reduce the total error  $E$  ?
  - Use Gradient Descent Method
  - Take the 1<sup>st</sup> order partial derivative of  $E$  with respect to weights
  - Adjust the weights  $\omega_{ij}$  and  $\omega_{jk}$

#### Backward Propagation

Use gradient descent of the error function  $E$  with respect to  $\omega_{jk}$  to adjust weights between **output** layer and **hidden** layer:

$$\frac{\partial E}{\partial Y_k} = 2 * \frac{1}{2} (Y_k - O_k) = Y_k - O_k$$

$$\frac{\partial E}{\partial X_k} = \frac{\partial E}{\partial Y_k} \frac{\partial Y_k}{\partial X_k} = \frac{\partial E}{\partial Y_k} Y_k (1 - Y_k) = (Y_k - O_k) Y_k (1 - Y_k)$$

$$\frac{\partial E}{\partial \omega_{jk}} = \frac{\partial E}{\partial X_k} \frac{\partial X_k}{\partial \omega_{jk}} = \frac{\partial E}{\partial X_k} Y_j = (Y_k - O_k) Y_k (1 - Y_k) Y_j \quad (6)$$

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.04.23 PM.png" style="zoom:50%;" />

$$E = \frac{1}{2} \sum_k (Y_k - O_k)^2$$

$$\omega_{jk,n} = \omega_{jk,n-1} - \rho * \frac{\partial E}{\partial \omega_{jk,n-1}} \quad (7)$$

where  $\rho$  is learning rate

Side Note:

The 1<sup>st</sup> order derivative of Sigmoid function:

$$y = \frac{1}{1 + e^{-x}} \Rightarrow \frac{dy}{dx} = (1 - y)y$$

#### Backward Propagation (cont'd)

Use gradient descent of the error function  $E$  with respect to  $\omega_{ij}$  to adjust weights between **hidden layer** and **input layer**:

$$\frac{\partial E}{\partial Y_j} = \sum_{k=1}^{n_k} \frac{\partial E}{\partial X_k} \frac{\partial X_k}{\partial Y_j} = \sum_{k=1}^{n_k} \frac{\partial E}{\partial X_k} \omega_{jk} = \sum_{k=1}^{n_k} (Y_k - O_k) Y_k (1 - Y_k) \omega_{jk}$$

$$\frac{\partial E}{\partial X_j} = \frac{\partial E}{\partial Y_j} \frac{\partial Y_j}{\partial X_j} = \frac{\partial E}{\partial Y_j} Y_j (1 - Y_j) = Y_j (1 - Y_j) \sum_{k=1}^{n_k} (Y_k - O_k) Y_k (1 - Y_k) \omega_{jk}$$

$$\frac{\partial E}{\partial \omega_{ij}} = \frac{\partial E}{\partial X_j} \frac{\partial X_j}{\partial \omega_{ij}} = \frac{\partial E}{\partial X_j} I_i = I_i Y_j (1 - Y_j) \sum_{k=1}^{n_k} (Y_k - O_k) Y_k (1 - Y_k) \omega_{jk} \quad (8)$$

$$\omega_{ij,n} = \omega_{ij,n-1} - \rho * \frac{\partial E}{\partial \omega_{ij,n-1}} \quad (9)$$

where  $\rho$  is learning rate

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.04.42 PM.png" style="zoom:50%;" />

$$E = \frac{1}{2} \sum_k (Y_k - O_k)^2$$

#### Numerical Example

We use a simple neural network as follows to show Forward and Backward propagation operations with numerical data.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.05.23 PM.png" style="zoom:50%;" />

| Input layer:         | 3 neurons |
| -------------------- | --------- |
| Hidden layer:        | 2 neurons |
| Output layer:        | 1 neuron  |
| Activation Function: | Sigmoid   |
| Learning rate:       | 5.0       |

#### Example: Iteration 1

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.06.18 PM.png" alt="Screenshot 2026-04-25 at 5.06.18 PM" style="zoom:50%;" />

### Example: Iteration 2

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.08.36 PM.png" alt="Screenshot 2026-04-25 at 5.08.36 PM" style="zoom:50%;" />

### Summary of Training Process

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.10.42 PM.png" style="zoom:50%;" />

- Send an input data  $I_i$  to the neurons in the input layer
- Feed Forward propagation:
  - Calculate the output  $Y_k$
  - Given target output  $O_k$ , calculate total error  $E$
- Backward propagation:
  - Adjust each weight  $\omega_{jk}$  between output layer and hidden layer
  - Adjust each weight  $\omega_{ij}$  between hidden layer and input layer
- Repeat with a new input data

### Demo of Neural Network Training

#### Multilayer Perceptrons Neural Network

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.11.37 PM.png" style="zoom:50%;" />

- The thickness of each connection between two neurons is proportional to the magnitude of the connection.
- The training process is the matter of adjusting the weight matrix.

### Comments

- Layers are combined to describe the architecture of a neural network
- Modifications to network architecture impact its capacity and performance
- The output of each layer must fit the input of the next layer
- Advantages:
  - nonlinear mapping from input to output space
  - Strong anti-noise capability
- Disadvantages:
  - No statistical diagnosis, inference, confidence interval for each weight (compare to coefficients of a regression model)
  - Lack of systematic way and theoretical basis to determine an optimal structure of network

### Specification of Neural Networks

Determine the specification of a Neural Network via **hyperparameters** that decide the time and computational cost, define the structure of the neural network model, affect the model's prediction accuracy.

- Number of Layers

  - 1 input layer, 1 hidden layer, 1 output layer is good enough for most of problems

  - If hidden layers  $\geq 2$ , it is a deep neural network

- Number of Neurons in each layer

  - Number neurons in input and output layers are determined by the data

  - There is no clear rules to determine # neurons in hidden layers. A Rule of Thumb is 2/3 of sum of # neurons in input and output for a three-layer MLP model.

- Learning rate
- Stopping policy – cross validation

### Cross Validation

A common issue about training a predictive neural network is the **overfitting problem** shown in the graph below.

- Generalization (Training) error – blue curve
- Prediction error with test data set – red curve

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.14.56 PM.png" style="zoom:50%;" />

Overfitting problem

### Cross Validation (cont'd)

Cross validation ( $k$ -fold) procedure:

- Randomly divide the dataset into three parts:
  - a training set,
  - a validation set, and
  - a test set

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.15.21 PM.png" style="zoom:50%;" />

- The training set is used to fit/train the models
- The validation set is used to estimate prediction error for model selection, determine the hyperparameters
- The test set is used for assessment of final model
- A typical split might be 50% for training, and 25% each for validation and testing

### Overfitting Issue

To overcome overfitting issue, two general strategies are employed when fitting neural networks.

- **Slow Learning:** the model is fit in a somewhat slow iterative fashion, using gradient descent with very small value of  $\rho$ . The fitting process is then stopped when overfitting is detected.
- **Regularization:** penalties are imposed on the parameters, usually lasso or ridge method.

### Regularization and SGD

Gradient descent usually takes many steps to reach a local minimum. In practice, there are a number of approaches for accelerating the process.

- **Stochastic Gradient Descent (SGD)**

When  $n$  is large, instead of summing gradients over all  $n$  observations, we can sample a small fraction or minibatch of them each time we compute a gradient step. This process is known as SGD and is the state of the art for learning deep neural networks.

- **Regularization** is essential to avoid overfitting by augmenting the objective function with a penalty term:

$$R(\theta; \lambda) = - \sum_{i=1}^n \sum_{m=0}^9 y_{im} \log(f_m(x_i)) + \lambda \sum_j \theta_j^2.$$

This is **ridge regularization** using the cross-validation approach to determine  $\lambda$ . **Lasso regularization** is also popular as an additional form of regularization, or as an alternative to ridge.

### Regularization and SGD

- We can also use different values of  $\lambda$  for the groups of weights from different layers.
- The term **epochs** counts the number of times that the full training set has been processed.

Example:

The multilayer network used in the digit recognition problem (MNIST) has over 235,000 weights, which is around four times the number of training examples. For this network, the **minibatch** size was 128 observations per gradient update. 20% of the 60,000 training observations were used as a validation set in order to determine when training should stop. So, in fact 48,000 observations were used for training, and hence there are  $48,000/128 \approx 375$  minibatch **gradient updates per epoch**.

#### Regularization and SGD

We see that the value of the validation objective actually starts to increase by 30 epochs, so **early stopping** can also be used as an additional form of regularization.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.16.25 PM.png" style="zoom:50%;" />

### Dropout Learning

The idea is to randomly remove a fraction  $\phi$  of the neurons in a layer when fitting the model. This is done separately each time a training observation is processed. This prevents nodes from becoming over-specialized and can be seen as a form of regularization. In practice dropout is achieved by randomly setting the activations for the “dropped out” neurons to zero, while keeping the architecture intact. (similar idea as random forest)

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.17.05 PM.png" style="zoom:50%;" />

Left: a fully connected network. Right: network with dropout in the input and hidden layer. The nodes in grey are selected at random and ignored in an instance of training.

#### Network Tuning

A Neural Network requires tuning some hyperparameters that all have an effect on the performance:

- The **number of hidden layers**, and the **number of units per layer**. Modern thinking is that the number of units per hidden layer can be large, and overfitting can be controlled via the various forms of regularization.
- **Regularization** tuning parameters. These include the **dropout rate**  $\phi$  and the strength  $\lambda$  of lasso and ridge regularization and are typically set separately at each layer.
- Details of **stochastic gradient descent**. These include the **batch size**, the **number of epochs**, and if used, details of data augmentation.

#### Implementation of Neural Network 

Use existing Python libraries to code neural networks

- SKlearn
- Tensorflow
- Keras
- PyTorch, etc.

The following example uses Sklearn library to train a Perceptron neural network with built-in data set “iris” and perform prediction.

### Implementation of neural network with existing library

```
from sklearn import datasets
import numpy as np
iris = datasets.load_iris()
X = iris.data[:, [2, 3]]
y = iris.target
print('Class labels:', np.unique(y))
```

```
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
iris = datasets.load_iris()
X = iris.data[:, [2, 3]]
y = iris.target
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=1,
stratify=y)
```

#### Example with *Python* (cont'd)

```
sc = StandardScaler()
sc.fit(X_train)
sc.fit(X_test)
X_train_std = sc.transform(X_train)
X_test_std = sc.transform(X_test)

from sklearn.linear_model import Perceptron
from sklearn.metrics import accuracy_score

ppn = Perceptron(n_iter=40, eta0=0.1, random_state=1)
ppn.fit(X_train_std, y_train) ##This is training the model
y_pred = ppn.predict(X_test_std) ##Test/Validating the model

print('Misclassified samples: %d' % (y_test != y_pred).sum())
print('Accuracy: %.2f' % accuracy_score(y_test, y_pred))
print('Accuracy: %.2f' % ppn.score(X_test_std, y_test))
```

# Deep Learning (II)

## Deep Neural Network

One input layer + many hidden layers + output layer

- Approximate complex nonlinear relationship, feature transformation
- A hidden layer is viewed as a linear model, a stack of linear models

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.19.22 PM.png" style="zoom:50%;" />

For example: CNN, RNN, Elman, Jordan, Boltzmann, etc.

## CONVOLUTIONAL NEURAL NETWORKS

Convolutional neural networks (CNNs) are being widely used in computer vision, digit recognition, image classification and natural language processing. The major differences between conventional neuron networks and CNNs are the size and structure. The size of a CNN can be much larger, consisting of tens of layers, each layer has tens or thousands of neurons. The layers of CNNs are not necessarily fully connected.

### Convolutional Neural Networks

Neural networks around 2010 with big successes in image classification. A special family of neural networks, ***Convolutional Neural Networks***, (CNNs) has evolved for classifying images and has shown spectacular success on a wide range of problems.. CNNs mimic to some degree how humans classify images, by recognizing specific features or patterns anywhere in the image that distinguish each object class.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.19.56 PM.png" style="zoom:50%;" />

The network takes in the image and identifies local features. It then combines the local features (low-level features, such as small edges, patches of color) in order to create compound features (higher-level features, such as parts of ears, eyes, so on). These compound features contribute to the probability of any given output class label, such as “tiger”.

### Convolutional Neural Networks

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.20.19 PM.png" style="zoom:50%;" />

How does a convolutional neural network build up this hierarchy?

It achieves this with two specialized types of hidden layers, called **convolution** layers and **pooling** layers.

Convolution layers search for small patterns in the image, whereas pooling layers reduce dimension to select a prominent subset. Modern CNN architectures make use of many convolution and pooling layers.

### Preprocess Images to Feature Map

Around 2010, massive databases of labeled images were being accumulated, with ever-increasing numbers of classes, such as a well-known image database the *CIFAR100* database, which consists of 60,000 images labeled with 100 different classes.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.20.33 PM.png" style="zoom:50%;" />

Each image has a resolution of  $32 \times 32$  pixels, with three eight-bit numbers per pixel representing *red*, *green* and *blue*. The numbers for each image are organized in a three-dimensional array called a **feature map**. The first two axes are spatial (both are 32-dimensional), and the third is the *channel* axis, representing the three colors.

#### Preprocess Images to Feature Map

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.21.00 PM.png" alt="Screenshot 2026-04-25 at 5.21.00 PM" style="zoom:50%;" />

### CONVOLUTION OPERATION

#### Convolution Operation

- A convolution layer is made up via a large number of convolution **filters**. Each filter is a template that determines whether a **local feature** is present in an image.
- A convolution filter relies on a very simple operation, called a ***convolution***, which is basically equivalent to repeatedly multiplying matrix elements and then adding the results.
- Example: consider a very simple example of a  $4 \times 3$  image:

$$\text{Original Image} = \begin{bmatrix} a & b & c \\ d & e & f \\ g & h & i \\ j & k & l \end{bmatrix}$$

- Now consider a  $2 \times 2$  filter of the form  $\text{Convolution Filter} = \begin{bmatrix} \alpha & \beta \\ \gamma & \delta \end{bmatrix}$
- Convolve the image with the filter, we get the result

$$\text{Convolved Image} = \begin{bmatrix} a\alpha + b\beta + d\gamma + e\delta & b\alpha + c\beta + e\gamma + f\delta \\ d\alpha + e\beta + g\gamma + h\delta & e\alpha + f\beta + h\gamma + i\delta \\ g\alpha + h\beta + j\gamma + k\delta & h\alpha + i\beta + k\gamma + l\delta \end{bmatrix}$$

#### Convolution Operation

Convolution of image is to extract features from an input image.

Convolution is a mathematical operation that takes two inputs:

- An image matrix (volume) of dimension  $(h \times w \times d)$
- A filter  $(f_h \times f_w \times d)$

and produce a “Feature Map” matrix as output  $(h - f_h + 1) \times (w - f_w + 1) \times 1$

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.21.37 PM.png" style="zoom:50%;" />

#### Convolution Operation

We compute the convolution as follows:

Start with the top-left pixel of the output:

1. Place the filter on the top-left corner of the input image
2. Calculate the element-wise product of each corresponding pixel value
3. Sum the products to obtain the top-left pixel value of the output

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.21.53 PM.png" style="zoom:50%;" />

Next, shift the filter to the right by **one position** and repeat steps 2. and 3. to obtain the next pixel value of the output

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.22.20 PM.png" style="zoom:50%;" />

#### Convolution Operation

An example of the convolution of  $6 \times 6$  image matrix is shown as below:

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.23.34 PM.png" alt="Screenshot 2026-04-25 at 5.23.34 PM" style="zoom:50%;" />

- We can think of the filter weights as the parameters going from an input layer to a hidden layer, with one hidden neuron for each pixel in the convolved image.
- We can think of the original image as the input layer in a convolutional neural network, and the convolved images as the neurons in the first hidden layer.

#### Convolution Operation

A convolution layer is composed of  $N$  filters of the same size and depth. We convolve each filter with the input volume and get  $N$  outputs. The outputs are passed to some activation function, such as *ReLU*, for example. Finally, those  $N$  outputs is stacked together into a  $(h - f_h + 1) \times (w - f_w + 1) \times N$  feature maps.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.24.22 PM.png" style="zoom:50%;" />

##### Example

- If a  $2 \times 2$  submatrix of the original image resembles the convolution filter, then it will have a large value in the convolved image; otherwise, it will have a small value. Thus, the convolved image highlights regions of the original image that resemble the convolution filter.
- In general convolution filters are small  $\ell_1 \times \ell_2$  matrices, with positive integers that are not necessarily equal.

Convolution filters find **local features** in an image of tiger, such as edges and small shapes.

We apply the two small convolution filters in the middle. The convolved images highlight areas in the original image where details similar to the filters are found.

Specifically, the top convolved image highlights the tiger's **vertical** stripes, whereas the bottom convolved image highlights the tiger's **horizontal** stripes.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.24.41 PM.png" style="zoom:50%;" />

##### Example

- In a convolution layer, we use a whole bank of **predefined filters** to pick out a variety of differently-oriented edges and shapes in the image.
- Some additional details:
  - Since the input image is in color, it has three **channels** represented by a three-dimensional feature map (matrices). Each channel is a two-dimensional ( $32 \times 32$ ) feature map — one for **red**, one for **green**, and one for **blue**. A single convolution filter will also have three channels, one per color, each of dimension  $3 \times 3$ , with potentially different filter weights. The results of the three convolutions **are summed to** form a two-dimensional output feature map.
  - If we use  $K$  different convolution filters at this first hidden layer, we get  $K$  two-dimensional output feature maps, which together are treated as a single three-dimensional feature map. Each of the  $K$  output feature maps is seen as a separate channel of information, so now we have  $K$  channels in contrast to the three-color channels of the original input feature map.

##### Example

- Some additional details (cont'd):
  - The three-dimensional feature map is just like the *activations* in a hidden layer of a simple neural network, but organized and produced in a spatially structured way.
  - We typically apply the ReLU activation function to the convolved image. This step is sometimes viewed as a separate layer in the convolutional neural network, referred to as a *detector layer*.

#### Convolution Operation

**Convolution** is formally called **cross-correlation** in the mathematics literature.

Performing convolutions on images instead of directly connecting each pixel to the neural network units has two main advantages:

1. Reduces the number of parameters we need to learn. Instead of learning the weights connecting each input pixel, we only need to learn the weights of the filter in a lower dimensional space.
2. Preserves locality. We don't have to flatten the image matrix into a vector; thus the relative positions of the image pixels are preserved.

#### Strides

*Stride* is the number of pixels shifts over the input matrix. When the stride is 1 then we move the filters to 1 pixel at a time. When the stride is 2 then we move the filters to 2 pixels at a time and so on.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.25.42 PM.png" alt="Screenshot 2026-04-25 at 5.25.42 PM" style="zoom:50%;" />

#### Padding

Sometimes filter does not fit perfectly fit the input image. We have two options:

- Zero-padding, pad the picture with zeros so that it fits
- Valid padding, drop the part of the image where the filter did not fit and keeps only valid part of the image.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.26.04 PM.png" alt="Screenshot 2026-04-25 at 5.26.04 PM" style="zoom:50%;" />

padding applied to an image matrix with one pixel.

Notice the zeros in the outer rows and columns

#### Non-Linearity (ReLU)

ReLU stands for Rectified Linear Unit for a non-linear operation. The output is

$$f(x) = \max(0, x)$$

ReLU's purpose is to introduce non-linearity in CNN. Since the real-world data would want CNN to learn would be non-negative linear values. Other nonlinear functions such as **tanh** or **sigmoid** can also be used. However, ReLU is better than the other two.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.26.28 PM.png" style="zoom:50%;" />

### POOLING OPERATION

#### Pooling Operation

- After the convolutional layer, it is a common practice to pass these values into the next layer which is known as the ***pooling*** layer. Spatial pooling also called *subsampling* or *downsize sampling* which **reduces the dimensionality** of each feature matrix but retains important information.
- While there are a number of possible ways to perform pooling (e.g., Max Pooling, Average Pooling, Sum Pooling), the max pooling operation summarizes each non-overlapping (e.g., 2x2) block of pixels in an image using the maximum value in the (2x2) block.
- This reduces the size of the image by a factor of two in each direction, and it also provides some **location invariance**: i.e., as long as there is a large value in one of the four pixels in the block, the whole block registers as a large value in the reduced image.

#### Pooling Operation

Here is a simple example of max pooling:

$$\text{Max pool} \begin{bmatrix} 1 & 2 & 5 & 3 \\ 3 & 0 & 1 & 2 \\ 2 & 1 & 3 & 4 \\ 1 & 1 & 2 & 0 \end{bmatrix} \rightarrow \begin{bmatrix} 3 & 5 \\ 2 & 4 \end{bmatrix}$$

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.26.47 PM.png" style="zoom:50%;" />

### DATA AUGMENTATION

#### Data Augmentation

An additional important trick used with image modeling is data augmentation. Essentially, each training image is replicated many times, with each replicate randomly distorted in a natural way such that human recognition is unaffected.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.27.01 PM.png" style="zoom:50%;" />

The original image (leftmost) is distorted in natural ways to produce different images with the same class label. These distortions do not fool humans, and act as a form of regularization when fitting the CNN.

Typical distortions are zoom, horizontal and vertical shift, shear, small rotations, and in this case horizontal flips. At face value this is a way of increasing the training set considerably with somewhat different examples, and thus protects against overfitting.

#### Data Augmentation

- In fact, we can see this as a form of **regularization**: we build a cloud of images around each original image, all with *the same label*. This kind of fattening of the data is similar in spirit to ridge regularization.
- The stochastic gradient descent algorithms for fitting deep learning models repeatedly process randomly-selected batches of, say, 128 training images at a time.
- This works hand-in-glove with augmentation, because we can distort each image in the batch on the fly, and hence do not have to store all the new images.

## ARCHITECTURE OF A CONVOLUTIONAL NEURAL NETWORK

### Architecture of CNN

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.27.50 PM.png" alt="Screenshot 2026-04-25 at 5.27.50 PM" style="zoom:50%;" />

#### Fully Connected (FC) Layer

Flattened as FC layer **after pooling layer**

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.28.26 PM.png" style="zoom:50%;" />

The feature map matrices will be converted as vector  $(x_1, x_2, x_3, \dots)$ . With the fully connected layers, we combined these features together to create a model. Finally, we have an activation function such as *softmax* to classify the outputs, such as tiger, cat, dog, car, or truck etc.

### Convolutional Neural Networks

- Each subsequent convolve layer is similar to the first. It takes as input the three-dimensional feature map from the previous layer and treats it like a single multi-channel image. Each convolution filter learned has as many channels as this feature map.
- Since the channel feature maps are reduced in size after each pool layer, we usually increase the number of filters in the next convolve layer to compensate.
- Sometimes we repeat several convolve layers before a pool layer. This effectively increases the dimension of the filter.
- These operations are repeated until the pooling has reduced each channel feature map down to just a few pixels in each dimension. At this point the three-dimensional feature maps are **flattened** — the pixels are treated as separate units — and fed into one or more **fully-connected** layers before reaching the output layer, which is a *softmax* activation.

### Convolutional Neural Networks

#### Summary

- Preprocess images: convert each image into a 3-channel matrices
- Feed our input image into the convolutional layer.
- **Convolutional layers:** perform convolution on the image. Choose parameters for convolution including stride, padding, and filter size. Add as many convolutional layers as possible until satisfied. Apply *ReLU* activation to the matrix.
- **Pooling Layers:** perform pooling on the output to reduce the dimension.
- **FC Layers:** flatten the output of the last pooling layer and feed into a fully connected layer; output the class using an activation function such as *softmax* function.

### Parallel Computation

Since the CNN models are typically very large, model **parallelization** is often necessary. In some cases, even a single layer of neurons cannot fit in a single machine's memory. The first way of parallelizing the model is to store each layer on a different machine.

In a forward pass, each machine receive data from the input machine, compute the output and pass it to the machine holding the next layer.

In a backward pass, each machine receives gradients from the next machine, compute the gradients of its parameters and feed them back to the machine holding the previous layer.

For a fully connected layer, there can be so many parameters that even splitting them onto several machines is necessary. In this case, communications happen if there is a forward or backward pass across the split boundaries.

### Convolutional Neural Networks

To fit large CNNs, it is common to use a **parameter server** to hold all model parameters. Several machines will then work as a bank, each bank has a replica of model from the parameter server, compute gradient and send the gradients back to the **model server**. Each bank of machines performs computation on a **stale model**. Each bank has an iteration number. When it tries to update the model, the update can be rejected if the stale model is too old.

Since there are too many parameters in a CNN, it is prone to overfitting. There are several heuristics of preventing this from happening. For example, we can use **regularization** when training the network. Another approach is **dropout**, which deactivates some neurons with some probability when training.

## RECURRENT NEURAL NETWORKS

### Recurrent Neural Networks

Many data sources are sequential in nature and call for special treatment when building predictive models. Examples include:

- Documents such as book and movie reviews, newspaper articles, and tweets. The sequence and relative positions of words in a document capture the narrative, theme and tone, and can be exploited in tasks such as *topic classification, sentiment analysis, and language translation*.
- Time series of temperature, rainfall, wind speed, air quality, and so on. We may want to *forecast the weather several days ahead*, or climate several decades ahead.
- Financial time series, where we track market indices, trading volumes, stock and bond **prices**, and exchange rates. Here prediction is often difficult, but as we will see, certain *indices can be predicted* with reasonable accuracy.
- Recorded speech, musical recordings, and other sound recordings. We may want to give a *text transcription of a speech*, or perhaps a *language translation*. We may want to assess the quality of a piece of music or assign certain attributes.

### Recurrent Neural Networks

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.29.32 PM.png" style="zoom:50%;" />

The figure illustrates the structure of a very basic RNN with a sequence  $X = \{X_1, X_2, \dots, X_L\}$  as input, a simple scalar  $Y$  as output, and a hidden-layer sequence  $\{A_\ell\}_1^L = \{A_1, A_2, \dots, A_L\}$ . Each  $X_\ell$  is a **vector**;

- The sequence is processed one vector  $X_\ell$  at a time.
- The activations  $A_\ell$  in the hidden layer is calculated by taking as input the vector  $X_\ell$  and the activation vector  $A_{\ell-1}$  from the previous step in the sequence.
- Each  $A_\ell$  feeds into the output layer and produces a prediction  $O_\ell$  for  $Y$ .  $O_L$ , the last of these, is the most relevant.

### Recurrent Neural Networks

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.31.03 PM.png" style="zoom:50%;" />

Schematic of a detailed recurrent neural network

In detail, suppose each vector  $X_\ell$  of the input sequence has  $p$  components  $X_\ell^T = (X_{\ell 1}, X_{\ell 2}, \dots, X_{\ell p})$ , and the hidden layer consists of  $K$  units  $A_\ell^T = (A_{\ell 1}, A_{\ell 2}, \dots, A_{\ell K})$ .

- The matrix  $W$  contains  $K \times (p+1)$  shared weights  $w_{kj}$  for the input-to-hidden layers.
- The matrix  $U$  contains  $K \times K$  shared weights  $u_{ks}$  for the hidden-to-hidden layers.
- The vector  $B$  contains  $K + 1$  shared weights  $\beta_k$  for the output layer.

### Recurrent Neural Networks

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.32.32 PM.png" style="zoom:50%;" />

The activation  $A_{\ell K}$  is computed as

$$A_{\ell k} = g\left(w_{k0} + \sum_{j=1}^p w_{kj} X_{\ell j} + \sum_{s=1}^K u_{ks} A_{\ell-1,s}\right)$$

and the output  $O_{\ell}$  is computed as

$$O_{\ell} = \beta_0 + \sum_{k=1}^K \beta_k A_{\ell k}$$

for a quantitative response, or with an additional sigmoid activation function for a binary response.

### Recurrent Neural Networks

- Notice that the same weights  $W$ ,  $U$  and  $B$  are used as we process **each element** in the sequence, i.e., they are not functions of  $\ell$ . This is a form of weight sharing used by RNNs, and similar to the use of filters weight in convolutional neural networks.
- As we proceed from beginning to end, the activations  $A_\ell$  accumulate a history of what has been seen before, so that the learned context can be used for prediction.
- For regression problems the loss function for an observation  $(X, Y)$  is  $(Y - O_L)^2$  which only references the final output  $O_L = \beta_0 + \sum_{k=1}^K \beta_k A_{Lk}$ . Thus  $O_1, O_2, \dots, O_{L-1}$  are not used.
- When we fit the model, each element  $X_\ell$  of the input sequence  $X$  contributes to  $O_L$  via the chain and hence contributes **indirectly** to learning the shared parameters  $W$ ,  $U$  and  $B$  via the loss function.
- With  $n$  input sequence/response pairs  $(x_i, y_i)$ , the parameters are found by minimizing the sum of squares

$$\sum_{i=1}^n (y_i - o_{iL})^2 = \sum_{i=1}^n \left( y_i - \left( \beta_0 + \sum_{k=1}^K \beta_k g \left( w_{k0} + \sum_{j=1}^p w_{kj} x_{iLj} + \sum_{s=1}^K u_{ks} a_{i,L-1,s} \right) \right) \right)^2.$$

### Recurrent Neural Networks

- Since the intermediate outputs  $O_\ell$  are not used, one may well ask *why they are there at all?*
- First of all, they come for free and provide an evolving prediction for the output. Furthermore, for some learning tasks the response is also a sequence, and so the output sequence  $\{O_1, O_2, \dots, O_L\}$  is explicitly needed.

#### Example: Time Series Forecasting

We illustrate RNN use in a financial time series forecasting problem. The figure shows historical trading statistics from the New York Stock Exchange (1962-1986).

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.33.31 PM.png" style="zoom:50%;" />

#### Example: Time Series Forecasting

Predicting stock prices is useful for planning trading strategies. The measurements on day  $t$  are denoted by  $v_t, r_t, z_t$  for *log\_volume*, *DJ\_return* and *log\_volatility*. There are a total of  $T = 6,051$  such triples.

The day-to-day observations are not independent of each other. The series exhibit **autocorrelation** — in this case values nearby in time tend to be similar to each other.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.33.51 PM.png" style="zoom:50%;" />

The autocorrelation function for *log\_volume*. We see that nearby values are strongly correlated, with correlations above 0.2 as far as 20 days apart.

#### Example: RNN forecaster

- We wish to predict a value  $v_t$  from past values  $v_{t-1}, v_{t-2}, \dots$ , and also to make use of past values of the other series  $r_{t-1}, r_{t-2}, \dots$  and  $z_{t-1}, z_{t-2}, \dots$ .
- How do we represent this problem in terms of the structure of RNN?
- The idea is to extract many short mini-series of input sequences  $X = \{X_1, X_2, \dots, X_L\}$  with a predefined length  $L$  (called the lag), and a corresponding target  $Y$ . They have the form

$$X_1 = \begin{pmatrix} v_{t-L} \\ r_{t-L} \\ z_{t-L} \end{pmatrix}, X_2 = \begin{pmatrix} v_{t-L+1} \\ r_{t-L+1} \\ z_{t-L+1} \end{pmatrix}, \dots, X_L = \begin{pmatrix} v_{t-1} \\ r_{t-1} \\ z_{t-1} \end{pmatrix}, \text{ and } Y = v_t.$$

- Each  $X_i$  consists of the three measurements, a 3-vector.
- Each value of  $t$  makes a separate  $(X, Y)$  pair, for  $t$  running from  $L + 1$  to  $T$ .

#### Example: Comparison with AR model

- For the NYSE data we use the past five trading days to predict the next day's trading volume. Hence,  $L = 5$ . Since  $T = 6,051$ , we can create 6,046 such  $(X, Y)$  pairs.
- We fit this model with  $K = 12$  hidden units using the 4,281 training sequences, and then used it to forecast the 1,765 values of log\_volume in the test set. We achieve an  $R^2 = 0.42$  on the test data.
- A traditional autoregression (AR) linear model, construct a response vector  $y$  and a matrix  $M$  of predictors for least squares regression as follows:

$$\mathbf{y} = \begin{bmatrix} v_{L+1} \\ v_{L+2} \\ v_{L+3} \\ \vdots \\ v_T \end{bmatrix} \quad \mathbf{M} = \begin{bmatrix} 1 & v_L & v_{L-1} & \cdots & v_1 \\ 1 & v_{L+1} & v_L & \cdots & v_2 \\ 1 & v_{L+2} & v_{L+1} & \cdots & v_3 \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 1 & v_{T-1} & v_{T-2} & \cdots & v_{T-L} \end{bmatrix}$$

#### Example: Comparison with AR model

- Fitting a regression of  $y$  on  $M$ , we get a traditional autoregression (AR) linear model:

$$\hat{v}_t = \hat{\beta}_0 + \hat{\beta}_1 v_{t-1} + \hat{\beta}_2 v_{t-2} + \cdots + \hat{\beta}_L v_{t-L}$$

- and is called an order- $L$  autoregressive model, or simply AR( $L$ ).
- For the NYSE data, an AR model with  $L = 5$  achieves a test  $R^2$  of 0.41, slightly inferior to the 0.42 achieved by the RNN.

## Long Short-Term Memory (LSTM) Models

##### The Problem with Sequence Models

1. Vanishing/Exploding Gradients

In plain sequence models, the more time-steps we have, the more chances we have that backpropagation gradients are either exploding or vanishing.

2. The Problem of Long-Term Dependencies

When the gap between the relevant information and the time-step grows, RNNs become unable to connect the information.

Long Short-Term Memory networks (LSTMs) can overcome the above two problems. LSTMs are a special type of recurrent neural networks which are capable of learning long-term dependencies.

### Long Short-Term Memory (LSTM) Models

**Two tracks** of hidden-layer activations are maintained, so that when the activation  $A_\ell$  is computed, it gets input from hidden units both **further back in time**, and **closer in time** — a so-called *LSTM-RNN*. With long sequences, this *LSTM-RNN* overcomes the problem of early signals being washed out by the time they get propagated through the chain to the final activation vector  $A_L$ .

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.36.34 PM.png" style="zoom:50%;" />

## ELMAN NEURAL NETWORKS

#### Elman Neural Networks

Elman neural network is a recurrent neural network. In a recurrent neural network, neurons connect back to other neurons, information flow is multi-directional, so the activation of neurons can flow around in a loop. This type of neural network has a sense of time and memory of earlier networks states which enables it to learn sequences which vary over time, perform classification tasks and develop predictions of future states. As a result, recurrent neural networks are used for classification, stochastic sequence modeling and associative memory tasks.

#### Elman Neural Networks

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.38.08 PM-7163902.png" alt="Screenshot 2026-04-25 at 5.38.08 PM" style="zoom:50%;" />

#### Elman Neural Networks

Suppose we have a neural network consisting of only two neurons. The network has one neuron in each layer. Each neuron has a bias denoted by  $b_1$  for the first neuron, and  $b_2$  for the second neuron. The associated weights are  $w_1$  and  $w_2$  with activation function  $f_1$  and  $f_2$ . The output  $Y$  as a function of the input attribute  $X$  is given by:

$$Y = f_2 (w_2 f_1 (w_1 X + b_1) + b_2)$$

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.39.18 PM.png" style="zoom:50%;" />

#### Elman Neural Networks

There is a context neuron which feeds the activation from the hidden layer neuron back to that same neuron. The activation from the context neuron is delayed by one time step and multiplied by  $w_2$  before being fed back into the network. The output at time  $t$  is given by:

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.39.52 PM.png" style="zoom:50%;" />

$$Y[t] = f_2 (w_3 f_1 (w_1 X[t] + w_2 C + b_1) + b_2)$$

where,

$$C = Y_1[t - 1]$$

We see, in this simple example, that the hidden layer is fully connected to inputs and the network exhibits **recurrent** connections; and the use of **delayed** memory creates a more **dynamic** neural network system.

#### Elman Neural Networks

Elman neural networks are akin to the multi-layer perceptron augmented with one or more context layers. The number of neurons in the context layer is equal to the number of neurons in the hidden layer. In addition, the context layer neurons are fully connected to all the neurons in the hidden layer.

The neurons in the context layer are included because they remember the previous internal state of the network by storing hidden layer neuron values. The stored values are delayed by one time step; and are used during the next time step as additional inputs to the network.

Elman Neural Networks are useful in applications where we are interested in **predicting** the next output in given sequence. Their dynamic nature can capture time-dependent patterns. Elman networks are particularly useful for modeling **time series data**.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.40.18 PM.png" style="zoom:50%;" />

## JORDAN NEURAL NETWORKS

### Jordan Neural Networks

Jordan neural networks are similar to the Elman neural network. The only difference is that the context neurons are fed from the output layer instead of the hidden layer. The activation of the output nodes is recurrently copied back into the context nodes. This provides the network with a memory of its previous state.

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.40.30 PM.png" style="zoom:50%;" />

A simple Jordan neural network

### Jordan Neural Networks

Jordan Neural Networks appear capably of modeling time series data for prediction, and are useful for classification problems.

Standardize the attribute data prior to using a neural network model. Whilst there are no fixed rules about how to normalize inputs, here are four popular choices for an attribute  $x_i$ :

$$z_i = \frac{x_i - x_{min}}{x_{max} - x_{min}}$$

where

$$z_i = \frac{x_i - \bar{x}}{\sigma_x}$$

$SS_i$  is the sum of squares of  $x_i$ , and  $\bar{x}$  and  $\sigma^2$  are the mean and standard deviation of  $x_i$ .

$$z_i = \frac{x_i}{\sqrt{SS_i}}$$

$$z_i = \frac{x_i}{x_{max} + 1}$$

### RESTRICTED BOLTZMANN MACHINES

#### Restricted Boltzmann Machines

Restricted Boltzmann Machine (RBM) is an unsupervised learning model that approximates the *probability density function* of sample data. The “restricted” part of the name points to the fact that there are no connections between units in the same layer. The weights of the model are learned by **maximizing the likelihood function of the samples**.

Since it is used to approximate a *probability density function*, it is often referred to in the literature as a **generative model**. Generative learning involves making guesses about the probability distribution of the original input in order to reconstruct it.

A **deep belief network (DBN)** is a probabilistic generative multilayer neural network composed of several **stacked Restricted Boltzmann Machines**.

#### Restricted Boltzmann Machines

<img src="Slides_Final.assets/Screenshot 2026-04-25 at 5.41.13 PM.png" style="zoom:50%;" />

Graphical representation of an RBM model

It is composed of two layers in which there are a number of units with inner layer connections. Connections between layers are symmetric and bidirectional, allowing information transfer in **both directions**.

It has one visible layer containing four nodes and one hidden layer containing three nodes. The visible nodes are related to the input attributes so that for each unit in the visible layer, the corresponding attribute value is observable.

Visible layer node has binary state  $v_i = 0$  or  $v_i = 1$  that make stochastic decisions about whether to transmit that input or not.; hidden layer node contains binary state  $h_j = 0$  or  $h_j = 1$ . For each unit or node in the hidden layer, the corresponding value is unobservable and it needs to be inferred

#### Restricted Boltzmann Machines

The RBM is a probabilistic energy-based model, meaning the probability of a specific configuration of the visible and hidden units is proportional to the negative exponentiation of an energy function,  $E(v, h)$ . For each pair of a visible vector and a hidden vector the probability of the pair  $(v, h)$  is defined as follows:

$$P(v, h) = \frac{1}{Z} \exp -\tilde{E}(v, h)$$

where the denominator  $Z$  is a normalizing constant known as the partition function. The partition function sums over all possible pairs of visible and hidden variables is computed as:

$$Z = \sum_v \sum_h \exp -\tilde{E}(v, h)$$

It is therefore a normalizing constant such that  $P(v, h)$  defines a probability distribution over all possible pairs of  $v$  and  $h$ .

#### Restricted Boltzmann Machines

As there are no intra-layer connections within an RBM the energy of a joint configuration  $(v, h)$ , which defines a bipartite structure, is given by:

$$\tilde{E}(v, h) = - \sum_{i=1}^m \sum_{j=1}^n w_{ij} v_i h_j - \sum_{i=1}^m v_i b_i - \sum_{j=1}^n h_j d_j$$

where  $w_{ij}$  is the weight associated with the link between  $v_i$  and  $h_j$ . Intuitively, weights identify the correlation of the nodes. Larger weights imply a larger possibility that connected nodes **concur**. The parameters  $b_i$  and  $d_j$  are the biases of the  $j^{\text{th}}$  hidden and  $i^{\text{th}}$  visible nodes respectively; and  $m$  and  $n$  are the number of nodes in the visible and hidden layer.

Another way to think about a RBM is as a parametric model of the joint probability distribution of visible and hidden variables.

#### Restricted Boltzmann Machines

Since the hidden units of the RBM only connect to units **outside** of their specific layer, they are **mutually independent given the visible units**. The conditional independence of the units in the same layer is a nice property because it allows us to factorize the **conditional distributions of the hidden units** given the visible units as:

$$P(h|v) = \prod_j P(h_j|v) \quad \text{with} \quad P(h_j = 1|v) = \text{sigmoid} \left( \sum_i w_{ij} v_i + d_j \right)$$

The conditional distribution of the visible units can be factorized in a similar way:

$$P(v|h) = \prod_i P(v_i|h) \quad \text{with} \quad P(v_i = 1|h) = \text{sigmoid} \left( \sum_j w_{ij} h_j + b_i \right)$$

These conditional probabilities are important for the iterative updates between hidden and visible layers when training an RBM model. In practice,  $Z$  is difficult to calculate so computation of the joint distribution  $P(v, h)$  is typically intractable.

#### Restricted Boltzmann Machines

The goal in training an RBM is to adjust the parameters of the model, denoted by  $\Theta$ , so that the log-likelihood function using the training data is maximized. The gradient of **the log-likelihood** is:

$$\frac{\partial}{\partial \Theta} L(\Theta) = - \left\langle \frac{\partial \tilde{E}(v; \Theta)}{\partial \Theta} \right\rangle_{data} + \left\langle \frac{\partial \tilde{E}(v; \Theta)}{\partial \Theta} \right\rangle_{model}$$

where  $\langle \bullet \rangle_{data}$  represents the expectation of all visible nodes  $v$  in regard to the data distribution and  $\langle \bullet \rangle_{model}$  denotes the model joint distribution defined by  $P(v, h)$ .

## When to Use Deep Learning

*Should we discard all our older tools, and use deep learning on every problem with data?*

- Let's revisit our *Hitters* dataset where the goal is to predict the Salary of a baseball player with 263 players observations and 19 variables.
- Split the data into a training set of 176 players (two thirds), and a test set of 87 players (one third).
- Three methods were used to fit a regression model to these data.
  - A linear model that has 20 parameters.
  - The same linear model was fit with lasso regularization by 10-fold cross-validation. It selected a model with 12 variables having nonzero coefficients.
  - A neural network with one hidden layer consisting of 64 ReLU units was fit to the data by stochastic gradient descent with a batch size of 32 for 1,000 epochs, and 10% dropout regularization. This model has 1,345 parameters.

## When to Use Deep Learning

| Model             | # Parameters | Mean Abs. Error | Test Set $R^2$ |
|-------------------|--------------|-----------------|----------------|
| Linear Regression | 20           | 254.7           | 0.56           |
| Lasso             | 12           | 252.3           | 0.51           |
| Neural Network    | 1345         | 257.4           | 0.54           |

- Prediction results on the Hitters test data with three methods.
- Similar performance for all three models, which are all respectable.
- With great ease we obtained linear models that work well. However, we spent a fair bit of time fiddling with the configuration parameters of the neural network to achieve these results.
- Hence, in cases like this we are much better off following **the parsimony principle**: when faced with several methods that give roughly equivalent performance, **pick the simplest**.

## When to Use Deep Learning

- We have a number of very powerful tools at our disposal, including neural networks, random forests and boosting, support vector machines, general linear models, to name a few, and variants of these.
- If we can produce models with the simpler tools that perform at the same level as complex tools, Wherever possible, it makes sense to try the simpler models first, because they are likely to be easier to fit and understand, and potentially less fragile than the more complex approaches.
- Typically, we expect **deep learning** to be an attractive choice when the sample size of the training set is extremely large, and when interpretability of the model is not a high priority.