# Lecture 2 - 1/21/2025

### Search Engine Evaluation

How do we measure the quality of search engines?

- Precision = 
  - #(relevant items retrieved) 
    divided by 
    #(all retrieved items)
- Recall = 
  - #(relevant items retrieved)
    divided by
    #(all relevant items)

### Formalizing Precision/Recall

|               | Relevant            | Non-Relevant        |
| ------------- | ------------------- | ------------------- |
| Retrieved     | True positive (tp)  | False positive (fp) |
| Not retrieved | False negative (fn) | True negative (tn)  |

Precision = tp/(tp + fp) | Recall = tp/(tp + fn)

- The accuracy of an engine is defined as: 
  - the fraction of these classifications that are correct (tp + tn) / ( tp + fp + fn + tn)

**For web applications, Precision is more important than Recall**

### Precision/Recall Two Observations

- You can get high recall (but low precision) by retrieving all docs for all queries! 
  - a rather foolish strategy 
- In a good system, precision decreases as the number of docs retrieved (or recall) increases 
  - This is not a theorem, but a result with strong empirical confirmation 
  - E.g. viewing multiple pages of Google results often does not improve precision at all 

### Harmonic Mean

- There are three Pythagorean means 
  - 1. arithmetic mean, 2. geometric mean, 3. harmonic mean 
  - of course we all know how to compute the arithmetic mean 
  - the geometric mean is the nth root of the product of n numbers 
- The harmonic mean tends strongly toward the least element of the list making it useful in analyzing search engine results 
-  To find the harmonic mean of a set of n numbers 
  1. add the reciprocals of the numbers in the set 
  2. divide the sum by n 
  3. take the reciprocal of the result 
- e.g. for the numbers 3, 6, 9, and 12 
  - The arithmetic mean is: (3+6+9+12)/4 = 7.5 
  - The geometric mean is: nth-root(3x6x9x12) = 4th-root(1944) = 6.64
  - The harmonic mean is: (1/3+1/6+1/9+1/12)=(.33+.16+.11+.08)/4=0.17 and 1/0.17 = 5.88

### F Measure

- The harmonic mean of the precision and the recall is often used as an aggregated performance score for the evaluation of algorithms and systems: called the **F-score (or F-measure).**

- **Harmonic mean** of recall and precision is defined as:
  $$
  F = \frac{1}{\frac{1}{2} \left(\frac{1}{R} + \frac{1}{P}\right)} = \frac{2RP}{R + P}
  $$
  
  - The harmonic mean emphasizes the importance of small values, whereas the arithmetic mean is affected more by outliers that are unusually large.
  
- **More general form of F-Measure:**

  $$
  F_\beta = \frac{(\beta^2 + 1)RP}{R + \beta^2 P}
  $$

  - $\beta$ is a parameter that controls the relative importance of recall and precision.