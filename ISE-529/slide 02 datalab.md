

Predictive Analytics (ISE529)

# Predictive Modeling

Dr. Tao Ma  
ma.tao@usc.edu  
*2026 Spring*

## INTRODUCTION TO PREDICTIVE MODELS

### Statistical vs Machine Learning

- Machine learning arose as a subfield of Artificial Intelligence.
- Statistical learning arose as a subfield of Statistics.
- There is much **overlap** — both fields focus on supervised and unsupervised problems:
  - Machine learning has a greater emphasis on **large scale** applications and **prediction accuracy**.
  - Statistical learning emphasizes models and their **interpretability, precision** and **inference**.
- But the distinction has become more and more blurred, and there is a great deal of “cross-fertilization”.
- Machine learning has the upper hand in Marketing!

### A Brief History

- At the beginning of the 19<sup>th</sup> century, the method of **least squares** was developed, implementing the earliest form of **linear regression** for predicting **quantitative** values.
- **Linear discriminant analysis** was proposed in 1936 to predict **qualitative** values (categorical). In the 1940s, **logistic regression**
- In the early 1970s, the **generalized linear model** was developed to describe an entire class of statistical learning methods that include both **linear** and **logistic** regression
- In the mid 1980s, **classification** and **regression trees** were developed, followed shortly by **generalized additive models**.
- **Neural networks** gained popularity in the 1980s, and **support vector machines** arose in the 1990s.

Since that time, statistical learning has emerged as a new subfield in statistics, focused on supervised and unsupervised modeling and prediction.

### Examples of Prediction Problems

- Identify the risk factors for prostate cancer.
- Classify a recorded phoneme based on a log-periodogram.
- Predict whether someone will have a heart attack based on demographic, diet and clinical measurements.
- Customize an email spam detection system.
- Identify the numbers in a handwritten zip code.
- Classify a tissue sample into one of several cancer classes, based on a gene expression profile.
- Establish the relationship between salary and demographic variables in population survey data.
- Traffic volume prediction over highway network and urban road network
- Weather forecast, earthquake forecast, etc., . . . . .

### Supervised vs Unsupervised Learning

Statistical/machine learning refers to a vast set of tools for understanding data. These tools can be classified as **supervised** or **unsupervised**.

- Supervised learning involves building a statistical model for predicting an output based on inputs. For each observation of the predictor measurement(s)  $x_i$ ,  $i = 1, \dots, n$  there is an **associated response** measurement  $y_i$ . We wish to fit a model that relates the response to the predictors, with the aim of accurately predicting the response for future observations (**prediction**) or better understanding the relationship between the response and the predictors (**inference**), e.g., linear regression and logistic regression
- Unsupervised learning describes the situation where for every observation  $i = 1, \dots, n$ , we observe a vector of measurements  $x_i$  without associated response  $y_i$ . There are inputs **but no output**; nevertheless, we can learn relationships and structure from such data, e.g. cluster analysis.

### The Supervised Learning

Specifically,

- Outcome measurement  $Y$  (also called dependent variable, response, target).
- Vector of  $p$  predictor measurements  $X$  (also called inputs, regressors, covariates, features, independent variables).
- In the **regression** problem,  $Y$  is quantitative (e.g., price, blood pressure).
- In the **classification** problem,  $Y$  takes values in a finite, unordered set (survived/died, digit 0-9, cancer class of tissue sample).  $Y$  is also called categorical variable.
- We have training data  $(x_1, y_1), \dots, (x_N, y_N)$ . These are observations (examples, instances) of these measurements.

### Objectives and example

Based on the training data we would like to:

- Accurately predict unseen test cases.
- Understand which inputs affect the outcome, and how.
- Assess the quality of our predictions and inferences.

Example:

we examine a number of **factors** that relate to wages for a group of men from the Atlantic region of the United States. We wish to understand the association between an employee's **age** and **education**, as well as the **calendar year**, on his wage.

<img src="slide 02 datalab.assets/Screenshot 2026-03-02 at 3.33.01 PM.png" alt="Screenshot 2026-03-02 at 3.33.01 PM" style="zoom:80%;" />

#### Example

In certain cases, we may wish to predict a non-numerical value—that is, a **categorical or qualitative** output.

- A stock market data set that contains the daily movements in the Standard & Poor's 500 (S&P) stock index over a 5-year period between 2001 and 2005.
- The goal is to predict whether the index will *increase or decrease* on a given day, using the past 5 days' percentage changes in the index. This is known as a **classification problem**.

<img src="slide 02 datalab.assets/Screenshot 2026-03-02 at 3.34.59 PM.png" alt="Screenshot 2026-03-02 at 3.34.59 PM" style="zoom:80%;" />

### Unsupervised Learning

- No outcome variable, just a set of predictors (features) measured on a set of samples.
- Objective is fuzzy:
  - find groups of samples that behave similarly
  - find features that behave similarly
  - find linear combinations of features with the most variation
- Difficult to know how well you are doing.
- Different from supervised learning but can be useful as a pre-processing step for supervised learning.

#### Example

In the situations where we only observe input variables, with no corresponding output. We may wish to understand which types of individuals are similar to each other by grouping them according to their observed characteristics. This is known as a **clustering problem**.

- A gene expression data set consists of 6,830 gene expression measurements for each of 64 cancer cell lines.
- We want to determine whether there are groups, or clusters, among the cell lines based on their gene expression measurements.

<img src="slide 02 datalab.assets/Screenshot 2026-03-02 at 3.36.31 PM.png" alt="Screenshot 2026-03-02 at 3.36.31 PM" style="zoom:80%;" />Representation of the gene expression data set in a two-dimensional space,  $Z_1$  and  $Z_2$ . Cell lines corresponding to the same cancer type tend to be nearby in the two-dimensional space.

### Philosophy

- It is important to understand the ideas behind the various techniques, in order to know how and when to use them.
- One must understand the simpler methods first, in order to grasp the more sophisticated ones.
- It is important to accurately **assess the performance of a method**, to know how well or how badly it is working
- **Simpler methods often perform as well as fancier ones!**
- This is an exciting research area, having important applications in science, industry and finance.
- Statistical/Machine learning is a fundamental ingredient in the training of a modern data scientist.

## STATISTICAL LEARNING

### What is Statistical Learning?

Suppose that we are statistical consultants hired by a client to investigate the **association** between **advertising** and **sales** of a particular product. Our client cannot directly increase sales of the product, but adjust advertising budgets, thereby indirectly increasing sales. The data set looks like:

| #   | TV    | radio | newspaper | sales |
|-----|-------|-------|-----------|-------|
| 1   | 230.1 | 37.8  | 69.2      | 22.1  |
| 2   | 44.5  | 39.3  | 45.1      | 10.4  |
| 3   | 17.2  | 45.9  | 69.3      | 9.3   |
| ... | ...   | ...   | ...       | ...   |
| 199 | 283.6 | 42    | 66.2      | 25.5  |
| 200 | 232.1 | 8.6   | 8.7       | 13.4  |

**Our goal** is to develop an accurate model that can be used to predict sales on the basis of the three media budgets.

- Input variables = Advertising budgets
- output variable = Sales

$$\text{Sales} \approx f(\text{TV}, \text{Radio}, \text{Newspaper})$$

### What is Statistical Learning?

- We use  $X$  with subscript to denote the input variables.  $x_1$  = TV budget,  $x_2$  = the radio budget,  $x_3$  = the newspaper budget. The inputs also refer to as predictors, independent variables, features, predictor, or sometimes just variables.
- Sales is a response or target that we wish to predict, generically refer to as the response or dependent variable denoted by  $Y$ . ( $Y$  = sales)

<img src="slide 02 datalab.assets/Screenshot 2026-03-02 at 3.37.07 PM.png" alt="Screenshot 2026-03-02 at 3.37.07 PM" style="zoom:80%;" />

### What is Statistical Learning?

Suppose to predict income using years of education. A plot of shows income versus years of education for 30 individuals in the Income data set.

<img src="slide 02 datalab.assets/Screenshot 2026-03-02 at 3.37.36 PM.png" alt="Screenshot 2026-03-02 at 3.37.36 PM" style="zoom:80%;" />

$$\text{income} \approx f(\text{years of education})$$

The function  $f$  that connects the input variable to the output variable is in general unknown. We must estimate  $f$  based on the observed points.

More generally, suppose that we observe a quantitative response  $Y$  and  $p$  different predictors,  $x_1, x_2, \dots, x_p$ . We assume that there is some relationship between  $Y$  and  $\mathbf{X}^T = (x_1, x_2, \dots, x_p)$ ,

Now we write our model as

$$Y = f(\mathbf{X}) + \epsilon.$$

Here  $f$  is a fixed but **unknown** function of  $x_1, x_2, \dots, x_p$ , and  $\epsilon$  is a random error term, which is independent of  $\mathbf{X}$  and has mean zero and variance  $\sigma^2$ .

Take expectation on both sides, we get:

$$E(Y | X = x) = f(X)$$

#### Mathematical Notation

What is a good value for  $f(X)$  at any selected value of  $X$ , say  $X = 4$ ? There can be many  $Y$  values at  $X = 4$ . According to the model, we get:

$$f(4) = E(Y | X = 4)$$

$E(Y|X = 4)$  is the expected value (average) of  $Y$  given  $X = 4$ .

This ideal  $f(X) = E(Y | X = x)$  is called the **regression function**.

![A scatter plot showing a positive correlation between X and Y. A red regression curve is fitted to the data points. A vertical red line is drawn at X=4, and a red dot on the curve indicates the predicted value f(4) = E(Y | X = 4).](595e9fd7e96f6b95bbaa6e6a45c32682_img.jpg)

A scatter plot illustrating the regression function. The x-axis is labeled 'x' and ranges from 1 to 7. The y-axis is labeled 'y' and ranges from -2 to 6. A red curve represents the regression function  $f(X) = E(Y | X = x)$ . A vertical red line is drawn at  $X = 4$ , and a red dot on the curve at this x-value indicates the expected value  $E(Y | X = 4)$ .

A scatter plot showing a positive correlation between X and Y. A red regression curve is fitted to the data points. A vertical red line is drawn at X=4, and a red dot on the curve indicates the predicted value f(4) = E(Y | X = 4).

### Why Estimate $f$ ?

Two main reasons that we may wish to estimate  $f$ :

#### **Prediction**

A good  $f$  yields accurate predictions of  $Y$  at new points  $\mathbf{X}^T = (x_1, x_2, \dots, x_p)$ .

$$\hat{Y} = \hat{f}(\mathbf{X}),$$

where  $\hat{f}$  represents our estimate for  $f$  and  $\hat{Y}$  represents the resulting prediction for  $Y$ .

#### **Inference**

We can understand the association between  $Y$  and  $x_1, x_2, \dots, x_p$ , which components are important in explaining  $Y$ , and which are irrelevant.

Depending on the complexity of  $f$ , we may be able to understand how each component  $x_j$  of  $\mathbf{X}$  affects  $Y$  and to what extent.

### Why Estimate $f$ ?

#### Prediction

For instance, a company is interested in conducting a direct-marketing campaign. The goal is to identify individuals who are likely to respond positively to a mailing, based on observations of demographic variables measured on each individual.

- The demographic variables serve as predictors, and
- The response to the marketing campaign (either positive or negative) serves as the outcome.

The company is not interested in obtaining a deep understanding of the relationships between each individual predictor and the response; instead, the company simply wants to accurately predict the response using the predictors.

### Why Estimate $f$ ?

#### Inference

1. Consider the advertising data set, answer the following questions:

- Which media are associated with sales?
- Which media generate the biggest boost in sales?
- How large of an increase in sales is associated with a given increase in TV advertising?

2. Modeling the brand of a product that a customer might purchase based on variables such as price, store location, discount levels, competition price, and so forth. In this situation one might really be interested in the association between each variable and the probability of purchase. Answer the following questions:

- To what extent is the product's price associated with sales?

### Why Estimate $f$ ?

### Combination for prediction and inference

In a real estate setting, one may seek to relate **values of homes** to inputs such as crime rate, zoning, distance from a river, air quality, schools, income level of community, size of houses, and so forth.

Answer the following questions:

- How much extra will a house be worth if it has a view of the river? (inference)
- Is this house under- or over-valued given its characteristics? (prediction)

Depending on whether our ultimate goal is prediction, inference, or a combination of the two, different methods for estimating  $f$  may be appropriate to serve different purposes, e.g., linear models for interpretable inference; non-linear approaches for prediction.

### How to estimate $f$ ?

- In essence, statistical learning refers to a set of approaches for estimating  $f$ . We focus on the key theoretical concepts that arise in **estimating**  $f$ , as well as tools for **evaluating** the estimates obtained.  $f$  represents the relationship between  $X$  and  $Y$ .  $f$  must be determined by observed data.
- A set of  $n$  different data points is called the **training data set**.
- Let  $x_{ij}$  data represent the value of the  $j^{\text{th}}$  predictor, or input, for observation  $i$ , where  $i = 1, 2, \dots, n$  and  $j = 1, 2, \dots, p$ .
- Correspondingly, let  $y_i$  represent the response variable for the  $i^{\text{th}}$  observation.
- Then our training data consist of  $\{(x_1, y_1), (x_2, y_2), \dots, (x_n, y_n)\}$  where  $x_i^T = (x_{i1}, x_{i2}, \dots, x_{ip})$ .
- Our goal is to apply a statistical learning method to the training data in order to estimate the unknown function  $f$ , i.e., to find a function  $\hat{f}$  such that  $Y \approx \hat{f}(X)$  for any observation  $(X, Y)$ .

### How to estimate $f$ ?

Broadly speaking, most statistical learning methods for this task can be characterized as either **parametric** or **non-parametric**.

**Parametric Methods:** a two-step approach.

1. Make an assumption about the functional form, or shape of  $f$ .

*e.g.,  $f$  is linear in  $X$ :*

$$f(X) = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \cdots + \beta_p X_p.$$

Once we have assumed that  $f$  is linear, the problem of estimating  $f$  is boiled down to estimating the  $(p+1)$  coefficients  $\beta_0, \beta_1, \dots, \beta_p$ .

### How to estimate $f$ ?

2. After a model form has been selected, we need a procedure that uses the training data to fit or train the model, *i.e.*, find values of these parameters such that

$$Y \approx \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \cdots + \beta_p X_p.$$

The most common approach to fitting the model form above is referred to as (ordinary) **least squares**.

The potential disadvantage of a parametric approach is that the model we choose will usually not match the true unknown form of  $f$ .

### How to estimate $f$ ?

A linear model fit by least squares to the Income data . The observations are shown in red, and the yellow plane indicates the **least squares** fit to the data.

![3D scatter plot showing a linear regression fit.](c17eaf807acd5faec68da19dd16929be_img.jpg)

A 3D scatter plot illustrating a linear model fit. The vertical axis is labeled 'Income'. The two horizontal axes are labeled 'Years of Education' and 'Seniority'. Red dots represent individual data observations. A yellow grid plane represents the least squares fit to the data, showing a positive linear relationship between the predictors and income.

3D scatter plot showing a linear regression fit.

We have fit a linear model of the form

$$\text{income} \approx \beta_0 + \beta_1 \times \text{education} + \beta_2 \times \text{seniority}.$$

### How to estimate $f$ ?

**Non-parametric** methods do not make explicit assumptions about the functional form of  $f$ . It instead attempts to produce an estimate for  $f$  that is as close as possible to the observed data.

By avoiding the assumption of a particular functional form for  $f$ , they have the potential to accurately fit a wider range of possible shapes for  $f$ .

#### Disadvantage:

Since they do not reduce the problem of estimating  $f$  to a small number of parameters, it **requires a very large data set** in order to obtain an accurate estimate for  $f$ .

It suffers from overfitting problem. It may fit the training data well but **will not yield accurate predictions** of the response on new observations that were not part of the original training data set.

A smooth thin-plate *spline* fit to the Income data, the observations are displayed in red.

![A 3D surface plot showing a thin-plate spline fit to income data based on years of education and seniority. The vertical axis is labeled 'Income', the horizontal axis is 'Years of Education', and the depth axis is 'Seniority'. The surface is a smooth, undulating yellow grid. Red dots representing data points are scattered across the surface, mostly following its contours.](b86f4fd2c05bc69b4e99efd5f15b743d_img.jpg)

A 3D surface plot showing a thin-plate spline fit to income data based on years of education and seniority. The vertical axis is labeled 'Income', the horizontal axis is 'Years of Education', and the depth axis is 'Seniority'. The surface is a smooth, undulating yellow grid. Red dots representing data points are scattered across the surface, mostly following its contours.

### How to estimate $f$ ?

**Non-parametric methods: moving average filter**

$$\hat{f}(x_i) = \text{Ave}(Y \mid X \in N(x_i))$$

where  $N(x_i)$  is some neighborhood of  $x_i$ . The parameter is bin width  $q$ .

![A scatter plot with a moving average trend line showing data over time from 1950 to 1980.](484cfbdc05aee471306eeb11c0ee2543_img.jpg)

The figure is a scatter plot with a moving average trend line. The x-axis represents years from 1950 to 1980. The y-axis represents values in thousands, ranging from 3.5 to 6.0. The data points are represented by open squares, and the moving average trend is shown as a solid blue line. The trend line follows the general pattern of the data points, smoothing out the fluctuations.

| Year | Data (thousands) | Moving Average (thousands) |
|------|------------------|----------------------------|
| 1950 | 4.8              | 4.9                        |
| 1951 | 5.1              | 4.8                        |
| 1952 | 5.0              | 4.6                        |
| 1953 | 4.5              | 4.4                        |
| 1954 | 3.5              | 4.0                        |
| 1955 | 4.2              | 3.8                        |
| 1956 | 3.7              | 3.7                        |
| 1957 | 3.6              | 3.6                        |
| 1958 | 3.6              | 3.5                        |
| 1959 | 3.4              | 3.5                        |
| 1960 | 3.3              | 3.4                        |
| 1961 | 3.3              | 3.4                        |
| 1962 | 3.6              | 3.5                        |
| 1963 | 3.7              | 3.7                        |
| 1964 | 4.0              | 4.0                        |
| 1965 | 4.2              | 4.3                        |
| 1966 | 4.5              | 4.7                        |
| 1967 | 5.0              | 5.1                        |
| 1968 | 5.1              | 5.2                        |
| 1969 | 5.7              | 5.4                        |
| 1970 | 5.7              | 5.3                        |
| 1971 | 5.0              | 5.2                        |
| 1972 | 5.0              | 5.4                        |
| 1973 | 5.4              | 5.3                        |
| 1974 | 5.5              | 5.4                        |
| 1975 | 5.5              | 5.3                        |
| 1976 | 5.4              | 5.1                        |
| 1977 | 4.2              | 4.8                        |
| 1978 | 4.8              | 4.5                        |
| 1979 | 3.9              | 4.1                        |
| 1980 | 3.9              | 4.1                        |

A scatter plot with a moving average trend line showing data over time from 1950 to 1980.

Example: we use moving average filter to estimate trend  $m_t$  over years.

$$\hat{m}_t = (2q + 1)^{-1} \sum_{j=-q}^{q} X_{t-j}, \quad q + 1 \le t \le n - q.$$

How do we choose a model form of  $f$  between inflexible and flexible approaches, such as linear regression versus smoothing spline ?

![A scatter plot showing the tradeoff between flexibility and interpretability for various statistical learning methods. The y-axis is 'Interpretability' (High to Low) and the x-axis is 'Flexibility' (Low to High).](1b1bb497e39fcc025a3fc8bd4fc78d9a_img.jpg)

The figure is a scatter plot illustrating the tradeoff between flexibility and interpretability for various statistical learning methods. The vertical axis is labeled 'Interpretability' with 'High' at the top and 'Low' at the bottom. The horizontal axis is labeled 'Flexibility' with 'Low' on the left and 'High' on the right. The methods are plotted as follows:

| Method                      | Flexibility (Low to High) | Interpretability (High to Low) |
|-----------------------------|---------------------------|--------------------------------|
| Subset Selection            | Low                       | High                           |
| Lasso                       | Low                       | High                           |
| Least Squares               | Low                       | Medium-High                    |
| Generalized Additive Models | Medium                    | Medium                         |
| Trees                       | Medium                    | Medium                         |
| Bagging, Boosting           | Medium-High               | Medium-Low                     |
| Support Vector Machines     | High                      | Low                            |
| Deep Learning               | High                      | Low                            |

A scatter plot showing the tradeoff between flexibility and interpretability for various statistical learning methods. The y-axis is 'Interpretability' (High to Low) and the x-axis is 'Flexibility' (Low to High).

The figure above represents the tradeoff between flexibility and interpretability, using different statistical learning methods. In general, as the flexibility of a method increases, its interpretability decreases.

#### The rule of thumb

- When **inference** is the goal, there are clear advantages to using simple and relatively inflexible statistical learning methods.
- In some settings, however, we are only interested in **prediction**, and the interpretability of the predictive model is simply not of interest. It will be best to use the most flexible model available.
- **Surprisingly, this is not always the case!** We will often obtain more accurate predictions using a less flexible method. This may seem counter-intuitive. This phenomenon is due to the potential for **overfitting** in highly flexible methods.
- **Parsimony** versus black-box. We often prefer a simpler model involving fewer variables over a black-box predictor involving them all.

### Regression vs Classification

- Variables can be characterized as either **quantitative** or **qualitative** (also known as **categorical**).
- Quantitative variables take on numerical values, e.g., income, the value of a house, stock price, etc.
- Qualitative variables take on values in one of  $K$  different classes, or categories, e.g., marital status (married or not), travel mode choice, etc.
- Regression quantitative response - regression problems  
*e.g., least squares linear regression*
- Regression qualitative response - classification problems  
*e.g., logistic regression*
- We select statistical learning methods on the basis of whether the response is quantitative or qualitative. However, whether the **predictors** are qualitative or quantitative is generally considered less important. Most of the statistical learning methods can be applied **regardless of the predictor variable type** as long as they are properly coded.

## ASSESSING MODEL ACCURACY

### How to choose the best $f$ ?

**“All models are wrong, but some are useful.”**

a quote by British statistician George E. P. Box, published in 1976.

*There is no free lunch in statistics*: no one method dominates all others over all possible data sets. On a particular data set, one specific method may work best, but some other methods may work better on a similar but different data set. **Hence it is an important task to decide for any given set of data which method produces the best results.**

Selecting the best approach can be one of the most challenging parts of performing statistical learning in practice. We need to find a way to measure the Goodness of Fit of a model.

### Measuring the Goodness of Fit

To evaluate the performance of a statistical learning method on a given data set, we need to measure how well its predictions match the observed data.

In the regression setting, the most commonly-used measure is the mean squared error (**MSE**), given by

$$\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{f}(x_i))^2,$$

where  $\hat{f}(x_i)$  is the prediction that  $\hat{f}$  gives for the  $i^{\text{th}}$  observation,  $y_i$  is response value of the  $i^{\text{th}}$  observation. If the MSE is computed using the training data that was used to fit the model, it is called the **training MSE**.

### Measuring the Goodness of Fit

Suppose that we fit our statistical learning method on our training observations  $\{(x_1, y_1), (x_2, y_2), \dots, (x_n, y_n)\}$ , and we obtain the estimate  $\hat{f}$ .

If  $\hat{f}(x_i) \approx y_i$ ,  $i = 1, 2, \dots, n$ , then the **training MSE** is small. However, we are not interested in whether the **training MSE** is small, instead, we want to know whether  $\hat{f}(x_0) \approx y_0$ , where  $(x_0, y_0)$  is a **test observation previously unseen** in training data set.

We want to choose the method that gives the lowest **test MSE**, as opposed to the lowest training MSE. if we had a large number of **test observations**, we could compute

$$MSE = Ave\left(y_0 - \hat{f}(x_0)\right)^2$$

the **average squared prediction error** for these test observations  $(x_0, y_0)$ . We'd like to select the learning method for which the **test MSE** is smallest.

### Measuring the Goodness of Fit

*Why not use the training MSE to select model?*

There is no guarantee that the model with the lowest **training MSE** will also have the lowest **test MSE**. Roughly speaking, the problem is that many statistical methods specifically estimate coefficients so as to minimize the training set MSE. For these methods, the training set MSE can be quite small, but the test MSE is often much larger.

True  $f$  shown in black, three estimates of  $f$  are shown: the linear regression line (orange), and two smoothing spline fits (blue and green).

Training MSE (grey curve)  
Test MSE (red curve)

![Two plots illustrating the bias-variance trade-off. The left plot shows data points (circles) and three fitted curves: a black true function, an orange linear regression line, and two smoothing splines (blue and green). The right plot shows Mean Squared Error (MSE) versus Flexibility. The grey curve represents Training MSE, which decreases as flexibility increases. The red curve represents Test MSE, which follows a U-shape, indicating overfitting at high flexibility. A horizontal dashed line at MSE = 1.0 represents the irreducible error Var(ε).](010f64870d9b7d9e04dc4059b1cf5f45_img.jpg)

The figure consists of two plots. The left plot shows a scatter plot of data points (circles) and three fitted curves: a black solid line representing the true function  $f$ , an orange solid line representing the linear regression fit, and two smoothing spline fits in blue and green. The x-axis is labeled  $X$  and the y-axis is labeled  $Y$ . The right plot shows the Mean Squared Error (MSE) on the y-axis versus Flexibility on the x-axis. The grey curve represents the Training MSE, which decreases as flexibility increases. The red curve represents the Test MSE, which follows a U-shape, indicating overfitting at high flexibility. A horizontal dashed line at MSE = 1.0 represents the irreducible error  $\text{Var}(\epsilon)$ .

Two plots illustrating the bias-variance trade-off. The left plot shows data points (circles) and three fitted curves: a black true function, an orange linear regression line, and two smoothing splines (blue and green). The right plot shows Mean Squared Error (MSE) versus Flexibility. The grey curve represents Training MSE, which decreases as flexibility increases. The red curve represents Test MSE, which follows a U-shape, indicating overfitting at high flexibility. A horizontal dashed line at MSE = 1.0 represents the irreducible error Var(ε).

The grey curve displays the average training MSE as a function of flexibility for a number of smoothing splines. The red curve denotes the test MSE. The horizontal dashed line indicates  $\text{Var}(\epsilon)$ , the lowest achievable test MSE.

### Overfitting Phenomenon

- As the flexibility of the statistical learning method increases, there is a monotone decrease in the training MSE and a **U-shape** in the test MSE. This is a fundamental property of statistical learning that holds regardless of the data set at hand and regardless of the statistical method being used.
- As model flexibility increases, the training MSE will decrease, **but the test MSE may not**. When a given method yields a small training MSE but a large test MSE, it is said to be **overfitting** the data.
- This is because our statistical learning procedure is working too hard to find patterns in the training data, and may be **picking up some** patterns that are just caused by random chance (**noise**) rather than by true properties of the unknown function  $f$ .

![A line graph illustrating the overfitting phenomenon. The x-axis is labeled 'Flexibility' and ranges from 0 to 25. The y-axis is labeled 'Mean Squared Error' and ranges from 0.0 to 2.5. A red curve represents the test MSE, which follows a U-shape, starting at approximately 1.75 for flexibility 2, reaching a minimum of about 1.1 at flexibility 5, and then increasing to about 2.4 at flexibility 25. A gray curve represents the training MSE, which decreases monotonically from approximately 1.75 at flexibility 2 to about 0.3 at flexibility 25. A horizontal dashed line is drawn at a Mean Squared Error of 1.0. Data points are marked with colored squares: yellow squares at flexibility 2 for both curves, blue squares at flexibility 5 for both curves, and green squares at flexibility 20 for both curves. The green square for the test MSE is significantly higher than the green square for the training MSE at flexibility 20, illustrating overfitting.](bf30e154f82662d212f21fccdfa2980f_img.jpg)

| Flexibility | Training MSE (Gray Curve) | Test MSE (Red Curve) |
|-------------|---------------------------|----------------------|
| 2           | 1.75                      | 1.75                 |
| 5           | 0.90                      | 1.10                 |
| 20          | 0.30                      | 1.50                 |

A line graph illustrating the overfitting phenomenon. The x-axis is labeled 'Flexibility' and ranges from 0 to 25. The y-axis is labeled 'Mean Squared Error' and ranges from 0.0 to 2.5. A red curve represents the test MSE, which follows a U-shape, starting at approximately 1.75 for flexibility 2, reaching a minimum of about 1.1 at flexibility 5, and then increasing to about 2.4 at flexibility 25. A gray curve represents the training MSE, which decreases monotonically from approximately 1.75 at flexibility 2 to about 0.3 at flexibility 25. A horizontal dashed line is drawn at a Mean Squared Error of 1.0. Data points are marked with colored squares: yellow squares at flexibility 2 for both curves, blue squares at flexibility 5 for both curves, and green squares at flexibility 20 for both curves. The green square for the test MSE is significantly higher than the green square for the training MSE at flexibility 20, illustrating overfitting.

### Overfitting Phenomenon

![Two plots illustrating overfitting. The left plot shows data points (circles) and three fitted curves (black, orange, green) against X (0 to 100) and Y (2 to 12). The right plot shows Mean Squared Error (0.0 to 2.5) versus Flexibility (2 to 20), with a U-shaped curve and a horizontal dashed line at MSE = 1.0.](e714d8aca168c4854edebc4a4f2e9bd1_img.jpg)

The figure consists of two plots. The left plot shows a scatter plot of data points (circles) and three fitted curves: a black straight line, an orange curve, and a green highly flexible curve. The x-axis is labeled 'X' (0 to 100) and the y-axis is labeled 'Y' (2 to 12). The right plot shows the Mean Squared Error (MSE) on the y-axis (0.0 to 2.5) versus Flexibility on the x-axis (2 to 20). It features a red curve that increases as flexibility increases, a gray curve that decreases, and a horizontal dashed line at MSE = 1.0. Green squares mark specific points on the red and gray curves at flexibility values of approximately 22 and 20, respectively.

Two plots illustrating overfitting. The left plot shows data points (circles) and three fitted curves (black, orange, green) against X (0 to 100) and Y (2 to 12). The right plot shows Mean Squared Error (0.0 to 2.5) versus Flexibility (2 to 20), with a U-shaped curve and a horizontal dashed line at MSE = 1.0.

Another example: using a different true  $f$  that is much closer to linear. observe that the training MSE decreases monotonically as the model flexibility increases, and that there is a U-shape in the test MSE. However, because the truth is close to linear, the test MSE only decreases slightly before increasing again, so that the orange least squares fit is substantially better than the highly flexible green curve.

#### Overfitting Phenomenon

![Two plots illustrating the overfitting phenomenon. The left plot shows data points (circles) and three fitted curves (yellow, blue, green) on a coordinate system with X from 0 to 100 and Y from -10 to 20. The right plot shows Mean Squared Error (MSE) versus Flexibility, with training MSE (red curve) and test MSE (gray curve) both decreasing as flexibility increases, but the test MSE eventually increasing due to overfitting.](16c69c0dacd3c57ae91acd114e5f5bd2_img.jpg)

The figure consists of two plots. The left plot shows a set of data points (circles) and three fitted curves (yellow, blue, and green) on a coordinate system with X from 0 to 100 and Y from -10 to 20. The yellow curve is a simple linear fit, while the blue and green curves are more complex, non-linear fits that pass through more data points. The right plot shows the Mean Squared Error (MSE) versus Flexibility. The training MSE (red curve) starts high and decreases rapidly as flexibility increases. The test MSE (gray curve) also starts high and decreases, but it follows a different path, eventually increasing as flexibility continues to increase, indicating overfitting. A horizontal dashed line at MSE = 1 represents a baseline error level.

Two plots illustrating the overfitting phenomenon. The left plot shows data points (circles) and three fitted curves (yellow, blue, green) on a coordinate system with X from 0 to 100 and Y from -10 to 20. The right plot shows Mean Squared Error (MSE) versus Flexibility, with training MSE (red curve) and test MSE (gray curve) both decreasing as flexibility increases, but the test MSE eventually increasing due to overfitting.

Another example: using a different true  $f$  that is highly non-linear. The training and test MSE curves still exhibit the same general patterns, but now there is a rapid decrease in both curves before the **test MSE** starts to increase slowly.

An estimator should be “close” in some sense to the true value of the unknown parameter.

#### Definition

The point estimator  $\hat{\Theta}$  is an unbiased estimator for the parameter  $\theta$  if

$$E(\hat{\Theta}) = \theta$$

If the estimator is not unbiased, then the difference

$$E(\hat{\Theta}) - \theta$$

is called the **bias** of the estimator  $\hat{\Theta}$  .

This is equivalent to saying that the mean of the sampling distribution of  $\hat{\Theta}$  is equal to  $\theta$ . When an estimator is unbiased, the bias is zero; that is,  $E(\hat{\Theta}) - \theta = 0$  .

### Sample Mean and Variance are Unbiased.

- Suppose that  $X$  is a random variable with mean  $\mu$  and variance  $\sigma^2$ . Let  $X_1, X_2, \dots, X_n$  be a random sample of size  $n$  from the population represented by  $X$ .
- Show that the sample mean  $\bar{X}$  and sample variance  $S^2$  are unbiased estimators of  $\mu$  and  $\sigma^2$ , respectively.

$$\bar{X} = \frac{X_1 + X_2 + \dots + X_n}{n} \quad S^2 = \frac{1}{n-1} \sum_{i=1}^{n} (X_i - \bar{X})^2$$

If we consider all unbiased estimators of  $\theta$ , the one with the smallest variance is called the **minimum variance unbiased estimator**.

![A graph showing two probability density functions for unbiased estimators of a parameter theta. The x-axis is labeled theta. The first curve, labeled 'Distribution of \hat{\theta}_1', is taller and narrower, indicating a smaller variance. The second curve, labeled 'Distribution of \hat{\theta}_2', is shorter and wider, indicating a larger variance. Both curves are centered on the same vertical line representing the true parameter value theta.](54bab05b404ce895e109a02e758a548a_img.jpg)

A graph showing two probability density functions for unbiased estimators of a parameter theta. The x-axis is labeled theta. The first curve, labeled 'Distribution of \hat{\theta}\_1', is taller and narrower, indicating a smaller variance. The second curve, labeled 'Distribution of \hat{\theta}\_2', is shorter and wider, indicating a larger variance. Both curves are centered on the same vertical line representing the true parameter value theta.

For example, we wish to estimate the mean of a population, two possible unbiased estimators for  $\mu$ : the sample mean  $\bar{X}$  and a single observation from the sample, say,  $X_i$ , which one should we use?

#### The Bias-Variance Trade-Off

The **U-shape** test MSE curves turns out to be the result of **two competing properties** of statistical learning methods. The expected test MSE, for a given value  $x_0$ , can always be decomposed into the sum of three fundamental quantities: the variance of  $\hat{f}(x_0)$ , the squared bias of  $\hat{f}(x_0)$  and the variance of the error term  $\epsilon$ . That is,

$$E\left(y_0 - \hat{f}(x_0)\right)^2 = \text{Var}\left(\hat{f}(x_0)\right) + \left[\text{Bias}\left(\hat{f}(x_0)\right)\right]^2 + \text{Var}(\epsilon)$$

where

$$\text{Var}\left(\hat{f}(x_0)\right) = E\left(\hat{f}(x_0) - E\left[\hat{f}(x_0)\right]\right)^2$$

$$\text{Bias}\left(\hat{f}(x_0)\right) = f(x_0) - E\left[\hat{f}(x_0)\right]$$

$$\text{Var}(\epsilon) = E\left(y_0 - f(x_0)\right)^2$$

Here the notation  $E\left(y_0 - \hat{f}(x_0)\right)^2$  defines the **expected test MSE** at  $x_0$ , refers to the average test MSE that we would obtain if we repeatedly estimated  $f$  using a large number of training sets and tested each at  $x_0$ .

#### - Variance of a statistical learning method

Using different training data sets will result in a different  $\hat{f}$ . Variance refers to the amount by which  $\hat{f}$  would change if we estimated it using a different training data set. If a method has high variance, then small changes in the training data can result in large changes in  $\hat{f}$ . In general, more flexible statistical methods have higher variance.

#### - Bias of a statistical learning method

Bias refers to the error between the model and the true  $f$  that is introduced by approximating method chosen. Generally, more flexible methods result in less bias.

#### - Irreducible error of a statistical learning method

Variability associated with  $\epsilon$  also affects the accuracy of our predictions. This is known as the irreducible error, because no matter how well we estimate  $f$ , we cannot reduce the error introduced by  $\epsilon$ . The quantity  $\epsilon$  may contain unmeasured variables (information) that are useful in predicting  $Y$ .

#### Reducible and irreducible error

Consider a given estimate  $\hat{f}$  and a set of predictors  $X_0$ , which yields the prediction  $\hat{y}_0 = \hat{f}(X_0)$ . Then, it is easy to show that

$$\begin{aligned} E\left(y_0 - \hat{f}(x_0)\right)^2 &= E\left[f(x_0) + \varepsilon - \hat{f}(x_0)\right]^2 \\ &= \underbrace{E\left[f(x_0) - \hat{f}(x_0)\right]^2}_{\text{reducible}} + \underbrace{Var(\varepsilon)}_{\text{irreducible}} \end{aligned}$$

Can you show it is equal to the following?

$$= \underbrace{Var\left(\hat{f}(x_0)\right) + \left[Bias\left(\hat{f}(x_0)\right)\right]^2}_{\text{reducible}} + \underbrace{Var(\varepsilon)}_{\text{irreducible}}$$

As a general rule, as we use more flexible methods, the variance will increase, and the bias will decrease and vice versa. Good test set performance of a statistical learning method requires low variance as well as low squared bias.

![Three plots illustrating the bias-variance trade-off. Each plot shows Flexibility on the x-axis (log scale: 2, 5, 10, 20) and a performance metric on the y-axis. The red curve is MSE, the blue curve is Bias, and the orange curve is Variance. A dashed horizontal line represents Var(epsilon). A vertical dotted line indicates the flexibility level corresponding to the smallest test MSE.](0e2f908bcaa3136175994fcf0c9c1a9f_img.jpg)

The figure consists of three side-by-side plots illustrating the bias-variance trade-off. Each plot has 'Flexibility' on the x-axis (log scale: 2, 5, 10, 20) and a performance metric on the y-axis. The legend indicates: MSE (red curve), Bias (blue curve), and Var (orange curve). A dashed horizontal line represents  $\text{Var}(\epsilon)$ . A vertical dotted line indicates the flexibility level corresponding to the smallest test MSE.

| Flexibility | MSE (Red) | Bias (Blue) | Var (Orange) |
|-------------|-----------|-------------|--------------|
| 2           | ~2.1      | ~1.0        | ~0.05        |
| 5           | ~1.1      | ~0.05       | ~0.1         |
| 10          | ~1.2      | ~0.02       | ~0.2         |
| 20          | ~2.4      | ~0.01       | ~1.4         |

Three plots illustrating the bias-variance trade-off. Each plot shows Flexibility on the x-axis (log scale: 2, 5, 10, 20) and a performance metric on the y-axis. The red curve is MSE, the blue curve is Bias, and the orange curve is Variance. A dashed horizontal line represents Var(epsilon). A vertical dotted line indicates the flexibility level corresponding to the smallest test MSE.

Squared bias (blue curve), variance (orange curve),  $\text{Var}(\epsilon)$  (dashed line), and test MSE (red curve is the sum of these three quantities.) for the three data sets in previous examples. The vertical dotted line indicates the flexibility level corresponding to the smallest test MSE.

### The Classification Setting

In the classification setting, model accuracy measure needs some modifications because  $y_i$  is qualitative. Given that  $f$  is estimated on the basis of training observations  $\{(x_1, y_1), (x_2, y_2), \dots, (x_n, y_n)\}$ , where now  $y_1, \dots, y_n$  are qualitative. We use the **training error rate** to quantify the accuracy of our estimate  $\hat{f}$ .

$$\frac{1}{n} \sum_{i=1}^{n} I(y_i \neq \hat{y}_i)$$

where  $\hat{y}_i$  is the predicted class label for the  $i^{\text{th}}$  observation using  $\hat{f}$ . And  $I(y_i \neq \hat{y}_i)$  is an indicator variable that equals 1 if  $y_i \neq \hat{y}_i$  and zero if  $y_i = \hat{y}_i$ .

$$I = \begin{cases} 1 & \text{if } y_i \neq \hat{y}_i \text{ i.e., } y_i \text{ was misclassified} \\ 0 & \text{if } y_i = \hat{y}_i \text{ i.e., } y_i \text{ was correctly classified} \end{cases}$$

The **training error rate** computes the fraction of incorrect classifications.

### The Classification Setting

Similar to the regression setting, the **test error rate** associated with a set of test observations of the form  $(x_0, y_0)$  is given by

$$\text{Ave} (I(y_0 \neq \hat{y}_0))$$

where  $\hat{y}_0$  is the predicted class label that results from applying the classifier  $\hat{f}$  to the test observation with predictor  $x_0$ . And  $I(y_0 \neq \hat{y}_0)$  is an indicator variable.

$$I = \begin{cases} 1 & \text{if } y_0 \neq \hat{y}_0 \text{ i.e., } y_0 \text{ was misclassified} \\ 0 & \text{if } y_0 = \hat{y}_0 \text{ i.e., } y_0 \text{ was correctly classified} \end{cases}$$

The **test error rate** also computes the fraction of incorrect classifications. A good classifier is one for which the test error rate is smallest.

#### Example: Bayes Classifier

The Bayes Classifier simply assigns a test observation  $y_0$  with predictor vector  $x_0$  to the class  $j$  for which

$$\max_j \Pr(y_0 = j | X = x_0)$$

where  $\Pr(y_0 | x_0)$  is a conditional probability, i.e., it is the probability that  $y_0$  is assigned to class  $j$ , given the observed predictor vector  $x_0$ .

- For each value of  $X_1$  and  $X_2$ , the Bayes classifier outputs a different probability of the response being orange or blue.
- The purple dashed line represents the points where the probability is exactly 50 %, called the **Bayes decision boundary**.
- In general, the overall Bayes error rate is given by

$$1 - E \left( \max_j \Pr(y_0 = j | X = x_0) \right)$$

![A scatter plot illustrating the Bayes Classifier. The horizontal axis is labeled X1 and the vertical axis is labeled X2. The plot shows two classes of data points: orange circles and blue circles. A purple dashed line, representing the Bayes decision boundary, separates the two classes. The background is a light blue grid. The orange points are concentrated in the upper-left region, while the blue points are concentrated in the lower-right region. The purple dashed line is a non-linear boundary that separates the two classes with some overlap.](f9625fa3465b009051f85d91cfa1da7e_img.jpg)

A scatter plot illustrating the Bayes Classifier. The horizontal axis is labeled X1 and the vertical axis is labeled X2. The plot shows two classes of data points: orange circles and blue circles. A purple dashed line, representing the Bayes decision boundary, separates the two classes. The background is a light blue grid. The orange points are concentrated in the upper-left region, while the blue points are concentrated in the lower-right region. The purple dashed line is a non-linear boundary that separates the two classes with some overlap.

#### Example: KNN classifier

In theory we would always like to predict qualitative responses using the Bayes classifier, because the test error rate is always minimized. However, if we do not know the conditional distribution of  $Y$  given  $X$ , computing the Bayes classifier is impossible.

The  **$K$ -nearest neighbors ( $KNN$ )** classifier attempts to **estimate** the conditional distribution of  $Y$  given  $X$ , and then classify a given observation to the class with highest **estimated** probability.

Given a positive integer  $K$  and a test observation  $x_0$ , the  $KNN$  classifier

- first identifies the  $K$  points in the training data that are closest to  $x_0$ , (by Euclidean distance),  $N_0$  denotes  $K$  nearest points.
- then estimates the conditional probability for class  $j$  as the fraction of points in  $N_0$  whose response values equal  $j$  :

$$\Pr(Y = j | X = x_0) = \frac{1}{K} \sum_{i \in N_0} I(y_i = j).$$

- Finally,  $KNN$  assigns the test observation  $y_0$  to the class with the largest probability.

#### Example: KNN classifier

Euclidean distance, a.k.a,  $L^2$  norm:

$$d(p, q) = \|p - q\|_2 = \sqrt{\sum_{i=1}^{n} (q_i - p_i)^2}$$

$p, q$  = Euclidean vectors represent two points in Euclidean  $n$  dimensional space

![Two plots illustrating the KNN classifier. The left plot shows a black cross point surrounded by a green circle, with six blue and six orange training points. The right plot shows a KNN decision boundary on a grid of points, separating blue and orange classes.](8a4275b35551f2ec9825a1aa442c0db1_img.jpg)

Two plots illustrating the KNN classifier. The left plot shows a black cross point surrounded by a green circle, with six blue and six orange training points. The right plot shows a KNN decision boundary on a grid of points, separating blue and orange classes.

The training data set consists of six blue and six orange observations. Choose  $K=3$ ,  $KNN$  identifies the three nearest observations around black cross point, two blue points and one orange, resulting in estimated probabilities of  $2/3$  for the blue class and  $1/3$  for the orange class. Hence  $KNN$  will predict that the black cross belongs to the blue class. The right graph shows **KNN decision boundary** after applied the  $KNN$  at all the possible values for  $X_1$  and  $X_2$ .

#### KNN vs. Bayes classifier

Even though the true distribution is not known by the *KNN* classifier, the *KNN* decision boundary using  $K = 10$  is very close to that of the Bayes classifier.

KNN:  $K=10$

![A scatter plot illustrating the KNN classifier with K=10. The plot shows two classes of data points: orange circles and blue circles, plotted on a grid. The x-axis is labeled X1 and the y-axis is labeled X2. A solid black line represents the decision boundary, and a dashed purple line represents the Bayes classifier decision boundary. The two lines are very close, indicating that the KNN classifier with K=10 closely approximates the Bayes classifier.](6dda36bad0978e272ca0420b0902b73a_img.jpg)

The figure is a scatter plot on a grid. The horizontal axis is labeled  $X_1$  and the vertical axis is labeled  $X_2$ . The plot contains two classes of data points: orange circles and blue circles. A solid black line represents the decision boundary of the KNN classifier with  $K=10$ . A dashed purple line represents the decision boundary of the Bayes classifier. The two lines are very close to each other, demonstrating that the KNN classifier with  $K=10$  closely approximates the Bayes classifier.

A scatter plot illustrating the KNN classifier with K=10. The plot shows two classes of data points: orange circles and blue circles, plotted on a grid. The x-axis is labeled X1 and the y-axis is labeled X2. A solid black line represents the decision boundary, and a dashed purple line represents the Bayes classifier decision boundary. The two lines are very close, indicating that the KNN classifier with K=10 closely approximates the Bayes classifier.

#### KNN vs. Bayes classifier

The choice of  $K$  has a drastic effect on the  $KNN$  classifier.

KNN:  $K=1$

![Scatter plot showing KNN classification with K=1. The plot displays two classes of data points: orange circles and blue circles. A highly irregular, jagged black line represents the decision boundary, which follows the local distribution of the training points very closely, indicating high flexibility and high variance.](11a2ed9ad059f4289e4475247d633e88_img.jpg)

Scatter plot showing KNN classification with K=1. The plot displays two classes of data points: orange circles and blue circles. A highly irregular, jagged black line represents the decision boundary, which follows the local distribution of the training points very closely, indicating high flexibility and high variance.

When  $K = 1$ , the decision boundary is overly flexible. This corresponds to a classifier that has low bias but very high variance.

KNN:  $K=100$

![Scatter plot showing KNN classification with K=100. The plot displays the same two classes of data points as the previous figure. A much smoother, more linear black line represents the decision boundary, indicating that the classifier is less flexible and more generalizable.](e6d17113d3c65cc31531ae8a73fe011f_img.jpg)

Scatter plot showing KNN classification with K=100. The plot displays the same two classes of data points as the previous figure. A much smoother, more linear black line represents the decision boundary, indicating that the classifier is less flexible and more generalizable.

As  $K=100$ ,  $KNN$  becomes less flexible and produces a decision boundary that is close to linear. This corresponds to a low variance but high bias classifier.

### Variance and Bias in Classifiers

In general, as we use more flexible classification methods, the training error rate will decline but the test error rate may not. The graph plotted the  $KNN$  test and training errors as a function of  $1/K$ . As  $1/K$  increases, the method becomes more flexible.

![A line graph showing KNN training and test error rates as a function of 1/K. The x-axis is 1/K (ranging from 0.01 to 1.00) and the y-axis is Error Rate (ranging from 0.00 to 0.20). A horizontal dashed line is at approximately 0.13. The Training Errors (blue line) start at ~0.185 and decrease steadily to ~0.01. The Test Errors (orange line) start at ~0.19, decrease to a minimum of ~0.135 at 1/K ≈ 0.1, then increase to ~0.17 at 1/K = 1.0.](6752cee124f693bc4cebc66180f4f91f_img.jpg)

| $1/K$ | Training Errors | Test Errors |
|-------|-----------------|-------------|
| 0.01  | 0.185           | 0.190       |
| 0.02  | 0.145           | 0.175       |
| 0.05  | 0.115           | 0.150       |
| 0.10  | 0.095           | 0.135       |
| 0.20  | 0.060           | 0.145       |
| 0.50  | 0.065           | 0.170       |
| 1.00  | 0.010           | 0.165       |

A line graph showing KNN training and test error rates as a function of 1/K. The x-axis is 1/K (ranging from 0.01 to 1.00) and the y-axis is Error Rate (ranging from 0.00 to 0.20). A horizontal dashed line is at approximately 0.13. The Training Errors (blue line) start at ~0.185 and decrease steadily to ~0.01. The Test Errors (orange line) start at ~0.19, decrease to a minimum of ~0.135 at 1/K ≈ 0.1, then increase to ~0.17 at 1/K = 1.0.

As in the regression setting, the training error rate consistently declines as the flexibility increases. However, the test error exhibits a  $U$ -shape, (with a minimum at approximately  $K = 10$ ) before overfits.