# CSCI 570 Spring 2025 Homework 4

1. Solve the following recurrences by giving tight Θ-notation bounds in terms of $$n$$ for sufficiently large $$n$$.  Assume that $$T(\cdot)$$ represents the running time of an algorithm, i.e., $$T(n)$$ is positive and non-decreasing, and for small constants $$c$$ independent of $$n$$, $$T(c)$$ is also constant.
   **You need to give the answer and the analysis.** (10 points)
   
   (a)  
   $$
   T(n) = 9T\left(\frac{n}{5}\right) + n \log n
   $$
   
   (b)  
   $$
   T(n) = \sqrt{2025}T\left(\frac{n}{3}\right) + n^{\sqrt{2025}}
   $$
   
   (c)  
   $$
   T(n) = 9T\left(\frac{n}{3}\right) + n^2 \log n
   $$
   
   (d)  
   $$
   T(n) = 10T\left(\frac{n}{2}\right) + 2^n
   $$
   
   (e)  
   $$
   T(n) = 3T\left(\frac{n}{4}\right) + n \log^2 n
   $$

- **(a)**  
  $$
  T(n) = 9\,T\!\left(\frac{n}{5}\right) + n \log n
  $$
  - Compare $$f(n) = n \log n$$ with $$n^{\log_{5}(9)}$$.
  - $$\log_{5}(9) \approx 1.365$$. Since $$n^{1.365}$$ grows faster than $$n \log n$$,  
    by the Master Theorem,  
  $$
  T(n) = \Theta\bigl(n^{\log_{5}(9)}\bigr).
  $$

  **(b)**  
  $$
  T(n) = \sqrt{2025}\,T\!\left(\frac{n}{3}\right) + n^{\sqrt{2025}}
  $$
  - $$\sqrt{2025} = 45$$. So the recurrence is $$T(n) = 45\,T(n/3) + n^{45}$$.
  - Compare $$f(n) = n^{45}$$ with $$n^{\log_{3}(45)} \approx n^{3.465}$$.
  - Since $$n^{45}$$ is much larger,  
  $$
  T(n) = \Theta\bigl(n^{45}\bigr).
  $$

  **(c)**  
  $$
  T(n) = 9\,T\!\left(\frac{n}{3}\right) + n^2 \log n
  $$
  - Here $$n^{\log_{3}(9)} = n^2$$.
  - $$f(n) = n^2 \log n$$ is the “border case” ($$n^c \log^k n$$ form with $$c=2, k=1$$).
  - By the extended Master Theorem,  
  $$
  T(n) = \Theta\bigl(n^2 (\log n)^2\bigr).
  $$

  **(d)**  
  $$
  T(n) = 10\,T\!\left(\frac{n}{2}\right) + 2^n
  $$
  - Compare $$f(n) = 2^n$$ with $$n^{\log_{2}(10)} \approx n^{3.32}$$.
  - $$2^n$$ grows faster than any polynomial,  
  $$
  T(n) = \Theta\bigl(2^n\bigr).
  $$

  **(e)**  
  $$
  T(n) = 3\,T\!\left(\frac{n}{4}\right) + n (\log n)^2
  $$
  - Compare $$f(n) = n(\log n)^2$$ with $$n^{\log_{4}(3)} \approx n^{0.79}$$.
  - $$n(\log n)^2$$ is larger by more than a polynomial factor compared to $$n^{0.79}$$.
  - Thus,  

  $$
  T(n) = \Theta\bigl(n (\log n)^2\bigr).
  $$

2. Given a square matrix $$M$$ of size $$n \times n$$, where each row and each column is sorted in increasing order,  design a divide-and= conquer algorithm to find a given value $$k$$ in $$M$$. Assume that $$n$$ is a power of 2. 
   You need to:
   
   **(a)** Describe your algorithm. It **must** be a divide-and-conquer algorithm. No proof of correctness is needed. (5 points)
   
   **(b)** Give your algorithm’s recurrence relation for runtime complexity. Briefly explain it. (5 points)
   
   **(c)** Solve the recurrence relation using the Master Theorem. (5 points)
   
   Solution:
   
   (a) Algorithm (Divide and Conquer)  
   
   1. If $$n = 1$$, just compare the single element with $$k$$.  
   2. Let $$\text{pivot} = M\!\bigl(\tfrac{n}{2}, \tfrac{n}{2}\bigr)$$.  
      - If $$\text{pivot} = k$$, return "found."  
      - If $$\text{pivot} < k$$, discard the top-left $$\tfrac{n}{2} \times \tfrac{n}{2}$$ quadrant (all are $$\leq \text{pivot}$$) and recursively search the other three quadrants (top-right, bottom-left, bottom-right).  
      - If $$\text{pivot} > k$$, discard the bottom-right $$\tfrac{n}{2} \times \tfrac{n}{2}$$ quadrant and recursively search the other three quadrants (top-left, top-right, bottom-left).
   
   (b) Recurrence Relation  
   
   Each divide step yields up to 3 subproblems, each of size $$\tfrac{n}{2} \times \tfrac{n}{2}$$. The extra work is just the constant-time pivot comparison:
   $$
   T(n) = 3\,T\!\Bigl(\tfrac{n}{2}\Bigr) + O(1).
   $$
   
   (c) Solving the Recurrence (Master Theorem)  
   
   - $$a = 3$$, $$b = 2$$.  
   - $$\displaystyle \log_{b}(a) = \log_{2}(3)$$.  
   - The extra work $$f(n)$$ is $$O(1)$$, which is smaller than $$n^{\log_{2}(3)}$$.  
   
   By the Master Theorem,
   $$
   T(n) = \Theta\!\bigl(n^{\log_{2}(3)}\bigr).
   $$

3. Solve Kleinberg and Tardos, Chapter 5, Exercise 3. 

   Suppose you’re consulting for a bank that’s concerned about fraud detection, and they come to you with the following problem. They have a collection of n bank cards that they’ve confiscated, suspecting them of being used in fraud. Each bank card is a small plastic object, containing a magnetic stripe with some encrypted data, and it corresponds to a unique account in the bank. Each account can have many bank cards corresponding to it, and we’ll say that two bank cards are equivalent if they correspond to the same account. 

   It’s very difficult to read the account number off a bank card directly, but the bank has a high-tech “equivalence tester” that takes two bank cards and, after performing some computations, determines whether they are equivalent.

   Their question is the following: among the collection of n cards, is there a set of more than n/2 of them that are all equivalent to one another? Assume that the only feasible operations you can do with the cards are to pick two of them and plug them into the equivalence tester. Show how to decide the answer to their question with only O(n log n) invocations of the equivalence tester. 

   You need to: 

   (a) Describe your algorithm. It must be a divide-and-conquer algorithm. No proof of correctness is needed. (7 points)

   (b) Give your algorithm’s recurrence relation for runtime complexity. Briefly explain it. (3 points)

   (c) Solve the recurrence relation using the Master Theorem. (5 points)

Solution: 

(a) Divide-and-Conquer Algorithm (High-Level)  

1. Divide the set of $$n$$ cards into two halves, each of size $$n/2$$.  
2. Recursively find any candidate card with more than $$n/4$$ equivalent cards in the left half, and do the same for the right half.  
3. Combine: Check (using pairwise equivalence tests) which of the two candidates is actually a "majority" in the combined set (over $$n/2$$ cards).  
   - If neither has over $$n/2$$ equivalent cards, the answer is "no."  
   - Otherwise, "yes."

(b) Recurrence Relation  

Each divide step creates two subproblems of size $$n/2$$:
$$
T(n) = 2\,T\!\Bigl(\tfrac{n}{2}\Bigr) + O(n).
$$
The $$O(n)$$ term accounts for pairwise checks needed in the "combine" step.

(c) Solve via Master Theorem  

- $$a = 2$$, $$b = 2$$.  
- $$\log_{b}(a) = \log_{2}(2) = 1.$$  
- $$f(n) = O(n)$$ matches $$n^{\log_{2}(2)} = n^1 = n.$$  

Hence by the Master Theorem:
$$
T(n) = \Theta(n \log n).
$$

4. Emily has received a set of marbles as her birthday gift. She is trying to create a staircase shape with her marbles. A staircase shape contains k marbles in the kth row. Given n as the number of marbles, help her to figure out the number of rows of the largest staircase she can make. (Time complexity < O(n))
   For example, a staircase of size 4 looks like:
   ∗
   ∗ ∗
   ∗ ∗ ∗
   ∗ ∗ ∗ ∗
   (a) Describe your algorithm. It must be a divide-and-conquer algorithm. (5 points)
   (b) Give your algorithm’s recurrence relation for runtime complexity. Briefly explain it (5 points)
   (c) Solve the recurrence relation and state the overall time complexity. (5 points)

   Solution:

   (a) Divide-and-Conquer (Binary Search) Algorithm  

   1. We want the largest $$k$$ such that $$\tfrac{k(k+1)}{2} \leq n$$.  
   2. Use binary search on the range $$[1,\,n]$$:  
      - Let $$\text{mid} = \lfloor(\text{low} + \text{high})/2\rfloor$$.  
      - Compute $$\text{sum} = \frac{\text{mid}\,(\text{mid}+1)}{2}$$ in $$O(1)$$ time.  
      - If $$\text{sum} \leq n$$, move $$\text{low} = \text{mid}+1$$.  
      - Else move $$\text{high} = \text{mid}-1$$.  
   3. Continue until $$\text{low} > \text{high}$$. The best valid $$\text{mid}$$ is the answer.

   (b) Recurrence Relation  

   Each step splits the search range in half, taking $$O(1)$$ time to check:
   $$
   T(n) = T\!\Bigl(\tfrac{n}{2}\Bigr) + O(1).
   $$

   (c) Time Complexity  

   By Master Theorem, a = 1, b = 2, and f (n) = O(1). Therefore, $n^{\log_ba} = n^{log_2 1} = n^0 = 1$. Since f (n) = Θ(1), it is the case 2 of master theorem therefore, 
   $$
   T(n) = \Theta(\log n).
   $$
   So the overall time complexity is $$O(\log n)$$.