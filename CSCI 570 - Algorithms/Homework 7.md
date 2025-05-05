# CSCI 570 Spring 2025 Homework 7

### Problem 1

Jack has gotten himself involved in a very dangerous game called the octopus game where he needs to pass a bridge which has some unreliable sections. The bridge consists of 3n tiles as shown below. Some tiles are strong and can withstand Jack’s weight, but some tiles are weak and will break if Jack lands on them, leading to a fatal fall. We have been given this information in an array called `BadTile(3,n)` where `BadTile (j, i) = 1` if the tile is weak and 0 if the tile is strong. At any step Jack can move either to the tile exactly in front of him (i.e. from tile `(j, i)` to `(j, i + 1)`), or diagonally to the left or right (if they exist). (No sideways or backward moves are allowed and one cannot go from tile `(1, i)` to `(3, i + 1)` or from `(3, i)` to `(1, i + 1)`). Jack is allowed to start in any (strong) tile `(j, 1)` in the beginning and end at any (strong) tile `(j, n)` at the end.

Use dynamic programming to find out how many ways (if any) there are for Jack to pass this deadly bridge. In Fig. 1, we show an example of bad tiles in gray and one of the possible ways for Jack to safely cross the bridge alive.

<img src="Homework 7.assets/image-20250314160933811.png" alt="image-20250314160933811" style="zoom:80%;" />

1. Define (in plain English) subproblems to be solved. (2 points).
2. Write a recurrence relation for the subproblems. (3 points)
3. Using the recurrence formula in part b, write pseudocode using iteration to compute the total number of ways to safely cross the bridge. (4 points). Make sure you specify:
   - Base cases and their values.
   - Where the final answer can be found (e.g. `opt(n)`, or `opt(0,n)`, etc.).

###### Answer:

**1.** 

Define `ways(j, i)` to be the number of ways Jack can reach tile $(j, i)$ safely (i.e., without stepping on weak tiles). We will build up the solution for `ways(j, i)` for each column $i$ from 1 up to $n$, and each row $j \in \{1,2,3\}$.

------

**2.** 

If `BadTile(j, i) = 1`, then `ways(j, i) = 0` because tile $(j,i)$ is not safe.
 Otherwise, for `BadTile(j, i) = 0`,
$$
\text{ways}(j, i)
=
\text{ways}(j,\,i-1)
+ \mathbf{1}_{j>1}\,\text{ways}(j-1,\,i-1)
+ \mathbf{1}_{j<3}\,\text{ways}(j+1,\,i-1),
$$
where $\mathbf{1}_{j>1}$ is an indicator that is 1 if $j>1$ (so $(j-1)$ is a valid row) and 0 otherwise; similarly for $\mathbf{1}_{j<3}$.

------

**3.**

Let `ways[j][i]` be a 2D array (3 × n). Rows `j` in `{1,2,3}`, columns `i` in `{1..n}`.

```python
def CountSafePaths(BadTile, n):

    # 1. Initialize ways array to 0
    create 2D array ways[1..3][1..n], set all ways[j][i] = 0

    # 2. Base cases: ways[j][1]
    # Jack can start at any strong tile in column 1
    for j in 1 to 3:
        if BadTile(j, 1) == 0:
            ways[j][1] = 1

    # 3. Fill dp table column by column
    for i in 2 to n:
        for j in 1 to 3:
            if BadTile(j, i) == 1:
                ways[j][i] = 0        # tile is weak, no ways
            else:
                ways[j][i] = ways[j][i-1]
                if j > 1:
                    ways[j][i] += ways[j-1][i-1]
                if j < 3:
                    ways[j][i] += ways[j+1][i-1]

    # 4. Sum up ways in the last column n
    totalWays = 0
    for j in 1 to 3:
        totalWays += ways[j][n]

    return totalWays
```

- **Base Cases**: `ways[j][1] = 1` if tile $(j,1)$ is strong, else 0.
- **Final Answer**: Sum of `ways[j][n]` for $j \in \{1,2,3\}$.

This gives the total number of ways to cross safely from the first column to the last.



### Problem 2

Given n balloons, indexed from 0 to n − 1. Each balloon is painted with a number on it represented by array nums. You are asked to burst all the balloons. If the you burst balloon i you will get $nums[i − 1] × nums[i] × nums[i + 1]$ coins. Here left and right are adjacent indices of i. After the burst, the left and right then becomes adjacent. You may assume $nums[−1] = nums[n] = 1$ and they are not real therefore you cannot burst them. Design a dynamic programming algorithm to find the maximum coins you can collect by bursting the balloons wisely. Analyze the running time of your algorithm.

Example. If you have the nums = [3, 1, 5, 8]. The optimal solution would be 167, where you burst balloons in the order of 1, 5, 3 and 8. The array nums after each step is:
[3, 1, 5, 8] → [3, 5, 8] → [3, 8] → [8] → []
And the number of coins you get is 3 × 1 × 5 + 3 × 5 × 8 + 1 × 3 × 8 + 1 × 8 × 1 = 167.

1. Define (in plain English) subproblems to be solved. (2 points)
2. Write a recurrence relation for the subproblems (3 points)
3. Using the recurrence formula in part b, write pseudocode to find the solution.(2 points)
4. Make sure you specify (2 points)
   - Base cases and their values.
   - Where the final answer can be found.

5. What is the complexity of your solution? (1 point)

###### Answer:

**1.** 

Define $\text{dp}[l][r]$ as the maximum coins you can earn by bursting all the balloons strictly between indices $l$ and $r$. Here, $l$ and $r$ are boundaries that themselves cannot be burst; they just mark the edges for the subproblem.

------

**2.**

If we choose the last balloon to burst in the subarray $(l, r)$ to be $k$, where $l < k < r$, then the coins from that final burst are
$$
\text{nums}[l] \,\times\, \text{nums}[k] \,\times\, \text{nums}[r].
$$
Plus, we must have already burst all balloons in $(l, k)$ and all balloons in $(k, r)$. So:
$$
\text{dp}[l][r]
\;=\;
\max_{l < k < r}\,
\Bigl[
\text{dp}[l][k]
\;+\;
\text{nums}[l] \times \text{nums}[k] \times \text{nums}[r]
\;+\;
\text{dp}[k][r]
\Bigr].
$$
If $r = l+1$, there are no balloons in between, so $\text{dp}[l][r] = 0$.

------

**3.**

Let `n` be the length of `nums`. To handle the boundary conditions $\text{nums}[-1] = \text{nums}[n] = 1$, we can create an extended array `extended[0..n+1]` such that:

- `extended[0] = 1`,
- `extended[n+1] = 1`,
- `extended[i+1] = nums[i]` for `i` in `0..n-1`.

Then we define a 2D array `dp[0..n+1][0..n+1]`, initialized to 0.

```python
def MaxCoins(nums):
    # Step 1: Create extended array with boundary 1's
    let extended[0] = 1
    for i in 1 to n:
        extended[i] = nums[i-1]
    extended[n+1] = 1

    # Step 2: Initialize dp array
    create 2D array dp of size (n+2) x (n+2)
    for l in 0 to n+1:
        for r in 0 to n+1:
            dp[l][r] = 0

    # Step 3: Fill dp by increasing subproblem length
    for length in 2 to n+1:   # subarray length from (r-l)
        for l in 0 to n+1-length:
            r = l + length
            # Compute dp[l][r]
            for k in (l+1) to (r-1):
                dp[l][r] = max(dp[l][r], 
                               dp[l][k] 
                               + extended[l]*extended[k]*extended[r] 
                               + dp[k][r])

    # The final answer is dp[0][n+1]
    return dp[0][n+1]
```

- **Base cases**: When `r = l+1`, `dp[l][r] = 0` because there are no balloons to burst in between.
- **Final Answer**: `dp[0][n+1]`.

------

**4.**

- **Time Complexity**: We have a triple nested loop over $l$, $r$, and $k$, each up to $O(n)$, giving a total of $O(n^3)$.
- **Space Complexity**: We use a 2D table `dp` of size $(n+2)\times(n+2)$, i.e. $O(n^2)$ space.



### Problem 3

We are given an array A of size n and an array B of size m where n ≥ m. Our goal is to remove n − m elements from A, in such a way that that removing them will transform A to B. Notice that the relative order stays the same for the remaining elements.
As an example, let A = [3, 1, 1, 4, 4, 1] and B = [3, 1, 4, 1], then there are 4 ways to remove the elements:

- [3, **1**, 1, **4**, 4, 1],
- [3, 1, **1**, **4**, 4, 1],
- [3, **1**, 1, 4, **4**, 1],
- [3, 1, **1**, 4, **4**, 1].

Design a dynamic programming algorithm to find out the number of different ways to remove elements from A that will transform A to B. To qualify full credit, your algorithm needs to run in $O(mn)$ time, sub-optimal algorithm will receive at most 10 pts.

1. Define (in plain English) sub-problems to be solved. (3 pts)
2. Write a recurrence relation for the sub-problems and specify the base cases. (5 pts)
3. Analyze its runtime complexity and explain why. (2 pts)

###### Answer:

**1.**

Let $\text{dp}[i][j]$ be the number of ways that the first $i$ elements of $A$ can be reduced to form the first $j$ elements of $B$. In other words, how many distinct subsequences of $A[0..i-1]$ match $B[0..j-1]$.

------

**2.**

1. **If $A[i-1] \neq B[j-1]$**, then we cannot use the $i$-th element of $A$ to match the $j$-th element of $B$. Hence the number of ways is just the number of ways to form $B[0..j-1]$ from $A[0..i-2]$:
   $$
     \text{dp}[i][j] = \text{dp}[i-1][j].
   $$

2. **If $A[i-1] = B[j-1]$**, then we can either use the $i$-th element of $A$ to match the $j$-th element of $B$, or skip it. Thus:
   $$
     \text{dp}[i][j] = \text{dp}[i-1][j] \;+\; \text{dp}[i-1][j-1].
   $$

**Base Cases**:

- $\text{dp}[0][0] = 1$: There is exactly 1 way to form the empty subsequence of $B$ from the empty prefix of $A$.
- $\text{dp}[i][0] = 1$ for all $i$ (0 to $n$): The empty subsequence of $B$ can always be formed by deleting all elements of $A[0..i-1]$.
- $\text{dp}[0][j] = 0$ for all $j > 0$: We cannot form a nonempty $B$ if we have zero elements of $A$.

Putting this together:
$$
\text{dp}[i][j] \;=\;
\begin{cases}
  \text{dp}[i-1][j] 
    & \text{if }A[i-1] \neq B[j-1],\\[6pt]
  \text{dp}[i-1][j] + \text{dp}[i-1][j-1]
    & \text{if }A[i-1] = B[j-1].
\end{cases}
$$

------

**3.**

1. We have a 2D table `dp` of size $(n+1)\times(m+1)$.
2. Each entry `dp[i][j]` is computed in $O(1)$ time by using the recurrence.
3. Therefore, the total time complexity is **$O(nm)$**.

This meets the $O(mn)$ requirement.



### Problem 4

You are given an integer array A of size N , where each element in the array satisfies 1 ≤ A[i] ≤ N . The array may contain duplicate numbers. Your task is to determine the length of the longest consecutive subsequence that can be formed from A.

A subsequence is a sequence derived from A by removing some elements (possibly none) while keeping the order of the remaining elements unchanged. A consecutive subsequence is a special type of subsequence where the numbers appear in strictly increasing and consecutive order. In other words, it should be of the form [x, x + 1, x + 2, . . . ] for some integer x, meaning that every number in the sequence must be exactly one more than the previous number.

For example, consider the array A = [1, 2, 6, 4, 3, 2]. The sequence [2, 6, 3] is a valid subsequence but not a consecutive subsequence because 6 does not equal to 2 + 1. On the other hand, [1, 2] is a valid consecutive subsequence because all the numbers appear in strictly increasing consecutive order.

Your goal is to design an efficient dynamic programming algorithm to compute the maximum length of any consecutive subsequence in A. Given that N can be as large as $10^5$, your solution should be optimized to run efficiently within these constraints.

1. Define (in plain English) sub-problems to be solved. (2 points)
2. Write a recurrence relation for the sub-problems. (3 points)
3. Using the recurrence formula in part b, write an iterative pseudo-code to find the solution. Make sure you specify base cases. (2 points)

4. What is the complexity of your solution? (1 points)

###### Answer:

**1.**

Define $\mathit{dp}[x]$ to be the length of the longest consecutive subsequence encountered so far that ends with the value $x$. As we go through each element of $A$, we decide whether we can extend a subsequence that ended with $(x - 1)$ by the new $x$.

------

**2.**

When processing a new element $A[i]$:
$$
\mathit{dp}[\,A[i]\,] \;=\; \max\Bigl(\,\mathit{dp}[\,A[i]\,], \,\mathit{dp}[\,A[i]\!-\!1] + 1\Bigr).
$$
If $\mathit{dp}[\,A[i]\!-\!1]$ is undefined (or zero), then treat it as zero so that $\mathit{dp}[\,A[i]\,] = \max(\mathit{dp}[\,A[i]\,], 1)$.

------

**3.**

Assume $1 \le A[i] \le N$. We can store $\mathit{dp}$ in an integer array of length $N+1$, all initially zero.

```python
def LongestConsecutiveSubseq(A, N):
    create array dp of size (N+1), fill with 0
    maxLen = 0

    for i in 0 to N-1:
        x = A[i]
        # Extend from x-1 if possible
        dp[x] = max(dp[x], dp[x-1] + 1)
        maxLen = max(maxLen, dp[x])

    return maxLen
```

- **Base Cases**: `dp[x] = 0` initially for all `x`.
- **Answer**: `maxLen`, the maximum value in `dp[]` after processing all elements, is the length of the longest consecutive subsequence.

------

**4.**

1. **Time Complexity**: $O(N)$. Each element $A[i]$ requires a constant-time update in `dp`.
2. **Space Complexity**: $O(N)$ to store `dp` of size $(N+1)$.