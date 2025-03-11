# CSCI 570 Spring 2025 Homework 6

### Problem 1

Suppose you have a rod of length N , and you want to cut up the rod and sell the pieces in a way that maximizes the total amount of money you get. A piece of length $i$ is worth $p_i$ dollars ($1 ≤ i ≤ N $ ). Devise a Dynamic Programming algorithm to determine the maximum amount of money you can get by cutting the rod strategically and selling the cut pieces (Rod lengths are integers).

1. Define (in plain English) subproblems to be solved.

2. Write a recurrence relation for the subproblems.

3. Using the recurrence formula in part b, write pseudocode to find the solution. Make sure you specify

   (a) base cases and their values

   (b) where the final answer can be found.

4. What is the complexity of your solution?



**1. **
 Define $\text{bestRevenue}(k)$ as the maximum amount of money that can be obtained by cutting a rod of length $k$. Solving $\text{bestRevenue}(k)$ for every $k$ from $1$ to $N$ allows us to build up to the final answer.

------

**2. **
$$
\text{bestRevenue}(k) \;=\; \max_{1 \le i \le k}\;\bigl(p_i \;+\;\text{bestRevenue}(k - i)\bigr)
$$
Here, $p_i$ is the price of a piece of length $i$.

------

**3. **

```pseudocode
def RodCut(p, N):
    /*
    	p[i] represents the price for a rod piece of length i
    	N is the total length of the rod
    */
    Create array bestRevenue of size N+1
    bestRevenue[0] = 0             /* Base case */
    
    for k from 1 to N:
        currentBest = -∞
        for i from 1 to k:
            currentBest = max(currentBest, p[i] + bestRevenue[k - i])
        bestRevenue[k] = currentBest
    
    return bestRevenue[N]          /* Final answer */
```

- **Base Case**:
   $\text{bestRevenue}(0) = 0$, meaning no rod yields zero revenue.
- **Final Answer**:
   $\text{bestRevenue}(N)$.

------

**4. **
 The solution uses a nested loop up to $N$, making it $O(N^2)$ time complexity. 

And $O(N)$ space complexity for sorting the array bestRevenue.



### Problem 2

Alice and Bob are playing a turn-based game. It involves N stones placed in a row, numbered 0 to N − 1 from the left to the right. Each stone $i$ has a positive value $s_i$. On each player’s turn, they can remove either the leftmost stone or the rightmost stone from the row and receive points equal to the sum of the remaining stones’ values in the row. The winner is the one with the higher score when there are no stones remaining. Alice goes first in this game. Both players play to maximize their score by the end of the game. Devise a Dynamic Programming algorithm to return the maximum difference in score that Alice can achieve over Bob. Your algorithm must run in $O(N^2)$ time.

1. Define (in plain English) subproblems to be solved.

2. Write a recurrence relation for the subproblems.

3. Using the recurrence formula in part b, write pseudocode to find the solution. Make sure you specify

   (a) base cases and their values,

   (b) where the final answer can be found.

4. What is the complexity of your solution?

**1. **

Define $\text{dp}[L][R]$ as the maximum difference in score the player whose turn it is can achieve over the other player, given stones only in the segment $[L, R]$.

------

**2. **

Let $\text{sum}(L, R)$ be the sum of the values of stones from index $L$ to $R$. On a player’s turn:

- If they remove the leftmost stone $s_L$, they gain $\text{sum}(L+1,R)$ points right now, but then the opponent can achieve $\text{dp}[L+1][R]$. Hence the net difference for the current player is $  \bigl(\text{sum}(L+1,R)\bigr) - \text{dp}[L+1][R].$
- If they remove the rightmost stone $s_R$, they gain $\text{sum}(L,R-1)$ points, and the difference becomes $  \bigl(\text{sum}(L,R-1)\bigr) - \text{dp}[L][R-1].$

So,
$$
\text{dp}[L][R] \;=\; \max\Bigl(\,\text{sum}(L+1,R)\;-\;\text{dp}[L+1][R],\quad \text{sum}(L,R-1)\;-\;\text{dp}[L][R-1]\Bigr).
$$
Since $\text{sum}(L+1,R) = \text{sum}(L,R) - s_L$ and $\text{sum}(L,R-1) = \text{sum}(L,R) - s_R$, therefore:
$$
\text{dp}[L][R] \;=\; \max\Bigl(\,\text{sum}(L,R) - s_L - \text{dp}[L+1][R],\; \text{sum}(L,R) - s_R - \text{dp}[L][R-1]\Bigr).
$$

------

**3. **

Let `s[0..N-1]` be the stone values. First, compute a prefix-sum array `prefix[]` so that
$$
\text{sum}(L, R) = \text{prefix}[R+1] - \text{prefix}[L].
$$

```python
def MaxScoreDifference(s, N):
    # 1. Compute prefix sums for O(1) range-sum queries
    prefix[0] = 0
    for i in 1 to N:
        prefix[i] = prefix[i-1] + s[i-1]

    # 2. Create DP table dp[L][R], 0 <= L, R < N
    create 2D array dp of size N x N
    
    # Base cases: when L == R, only one stone -> removing it yields 0 points (no stones remain)
    for i in 0 to N-1:
        dp[i][i] = 0

    # 3. Fill dp for subarray lengths from 2 to N
    for length in 2 to N:
        for L in 0 to N-length:
            R = L + length - 1
            total = prefix[R+1] - prefix[L]         # sum(L, R)
            # Option 1: remove left stone
            scoreIfLeft = total - s[L] - dp[L+1][R]
            # Option 2: remove right stone
            scoreIfRight = total - s[R] - dp[L][R-1]
            dp[L][R] = max(scoreIfLeft, scoreIfRight)

    # 4. The answer: dp[0][N-1] 
    return dp[0][N-1]
```

- **Base Case**
   $\text{dp}[i][i] = 0$. If there is only one stone, removing it leaves no stones, so the current player scores 0 from the "remaining" stones.

- **Final Answer**
   $\text{dp}[0][N-1]$ gives the maximum difference in Alice’s score over Bob if both play optimally, starting with the full array of stones.

------

**4. **

- We fill an $\text{N} \times \text{N}$ DP table, and each entry is computed in $O(1)$ time (using prefix sums for quick range sums).
- **Overall Time Complexity**: $O(N^2)$.
- **Space:** $O(N^2)$, for storing the DP table.

### Problem 3

The Math Club consisting of n members hurries to line up in a straight line to take a group photo. Since the members are not positioned by height, the line is looking very messy. The club president decides to remove a few members so that the line follows a formation with the remaining members staying where they are. We say that $k$ members remaining in the line with heights $r1, r2, . . . , rk$ are in formation if $r1 < r2 < . . . < ri > . . . > rk$, for some $1 ≤ i ≤ k$. For example, if the initial sequence of heights in inches is
$$
(58, 60, 62, 65, 63, 61, 59, 57)
$$
then, removing member #5 and #7 gives us the formation:
$$
(58, 60, 62, 65, 61, 57)
$$
Give an algorithm that runs in $O(n^2)$ time to find the minimum number of members to remove from the line, so that we get a formation as described.

1. Define (in plain English) subproblems to be solved.

2. Write a recurrence relation for the subproblems.

3. Using the recurrence formula in part b, write pseudocode to find the solution. Make sure you specify

   (a) base cases and their values,

   (b) where the final answer can be found.

4. What is the complexity of your solution?

**1. **

For each index `i` in the array of heights, compute two values:

- `lis[i]`: The length of the longest strictly increasing subsequence ending at index `i`.
- `lds[i]`: The length of the longest strictly decreasing subsequence starting at index `i`.

------

**2. **

**(a) LIS Recurrence**
$$
\text{LIS}[i] = 1 \;+\; \max_{\substack{0 \le j < i \\ \text{height}[j] < \text{height}[i]}} \text{LIS}[j],
$$
or $1$ if there is no such $j$.

**(b) LDS Recurrence**
$$
\text{LDS}[i] = 1 \;+\; \max_{\substack{i < j \le n-1 \\ \text{height}[j] < \text{height}[i]}} \text{LDS}[j],
$$
or $1$ if there is no such $j$.

------

**3. **

Let `h[0..n-1]` be the array of heights.

```python
def min_removals(heights):
    n = len(heights)
    if n == 0:
        return 0
    
    # Compute LIS (longest increasing subsequence ending at i)
    lis = [1] * n
    for i in range(n):
        for j in range(i):
            if heights[j] < heights[i] and lis[j] + 1 > lis[i]:
                lis[i] = lis[j] + 1
    
    # Compute LDS (longest decreasing subsequence starting at i)
    lds = [1] * n
    for i in range(n-1, -1, -1):
        for j in range(i+1, n):
            if heights[j] < heights[i] and lds[j] + 1 > lds[i]:
                lds[i] = lds[j] + 1
    
    # Find the maximum valid formation length
    max_len = 0
    for i in range(n):
        current = lis[i] + lds[i] - 1  # subtract 1 to avoid double-counting the peak
        if current > max_len:
            max_len = current
    
    return n - max_len
```

**(a) Base Cases**

- `LIS[i] = 1` initially: the shortest strictly increasing subsequence ending at `i` is just the element `h[i]` by itself.
- `LDS[i] = 1` initially: the shortest strictly decreasing subsequence starting at `i` is the single element `h[i]`.

**(b) Final Answer**
 $\text{minRemovals} = n - \max_{0 \le i < n}(\text{LIS}[i] + \text{LDS}[i] - 1).$

------

**4.**

1. **Time Complexity**:
   - Computing `LIS`: For each `i`, we look back at `j < i`, giving $O(n^2)$.
   - Computing `LDS`: For each `i`, we look forward at `j > i`, another $O(n^2)$.
   - Overall, still $O(n^2)$.
2. **Space Complexity**:
   - We use two arrays of size $n$ for `LIS` and `LDS`.
   - Hence, **Space Complexity** is $O(n)$.

### Problem 4

Consider the 0-1 knapsack problem where you have infinitely many coins of each type. Namely, there are $n$ different types of coins. Coins of type $i$ have a weight of $w_i$ and a value of $v_i (1 ≤ i ≤ n)$. There is an unlimited supply of coins of each type. Design a dynamic programming algorithm to compute the optimal value you can achieve with a knapsack that has a maximum weight capacity of $W$.

1. Define (in plain English) subproblems to be solved.
2. Write a recurrence relation for the subproblems.
3. Using the recurrence formula in part b, write pseudocode to find the solution. Make sure you specify

   (a) base cases and their values,

   (b) where the final answer can be found.

4. What is the complexity of your solution?

**1.**

Define `dp[x]` to be the maximum total value achievable with a knapsack capacity of exactly `x`. We will compute `dp[x]` for all `x` from `0` to `W`.

------

**2.**

For each capacity `x` and coin type `i`, if `w_i ≤ x`, we can consider using coin `i` one more time. So:
$$
\text{dp}[x] \;=\; \max\bigl(\text{dp}[x],\;\text{dp}[x - w_i] + v_i\bigr)\quad\text{for each }i\text{ such that }w_i \le x.
$$

------

**3. **

```python
def UnboundedKnapsack(n, W, w[], v[]):
    # n = number of coin types
    # W = maximum capacity
    # w[i], v[i] = weight, value of coin type i
    
    Create array dp of size W+1
    for x from 0 to W:
        dp[x] = 0
    
    for x from 0 to W:
        for i from 1 to n:
            if w[i] <= x:
                dp[x] = max(dp[x], dp[x - w[i]] + v[i])
    
    return dp[W]
```

**(a) Base Case**

- `dp[0] = 0`, meaning if the capacity is zero, the maximum value is zero.

**(b) Final Answer**

- The solution is in `dp[W]`.

------

**4. **

- **Time Complexity**: $O(n \times W)$, since we iterate over capacities up to $W$ and consider $n$ coin types for each capacity.
- **Space Complexity**: $O(W)$ for the `dp` array.