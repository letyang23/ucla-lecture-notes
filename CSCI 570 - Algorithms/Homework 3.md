# CSCI 570 Spring 2025 Homework 3

1. You are consulting for a trucking company that does a large amount of business shipping packages between New York and Boston. The volume is high enough that they have to send a number of trucks each day between the two locations. Trucks have a fixed limit $W$ on the maximum amount of weight they are allowed to carry. Boxes arrive at the New York station one by one, and each package $i$ has a weight $w_i$. The trucking station is quite small, so at most one truck can be at the station at any time. Company policy requires that boxes are shipped in the order they arrive; otherwise, a customer might get upset upon seeing a box that arrived after his make it to Boston faster. At the moment, the company is using a simple greedy algorithm for packing: they pack boxes in the order they arrive, and whenever the next box does not fit, they send the truck on its way.
   But they wonder if they might be using too many trucks, and they want your opinion on whether the situation can be improved. Here is how they are thinking. Maybe one could decrease the number of trucks needed by sometimes sending off a truck that was less full, and in this way allow the next few trucks to be better packed.
   Prove that, for a given set of boxes with specified weights, the greedy algorithm currently in use actually minimizes the number of trucks that are needed. Your proof should follow the type of analysis we used for the Interval Scheduling Problem: it should establish the optimality of this greedy packing algorithm by identifying a measure under which it “stays ahead” of all other solutions.

   **Answer:**
   
   The proof is similar to that for the interval scheduling solution we did in lecture. We first show (using mathematical induction) that the partition of boxes in our greedy solution is always "as far along" (or not behind) the partition of any optimal solution. Using this fact, we can then show that our solution is optimal (using proof by contradiction).
   
   1. Our trucks are always as far along as (or not behind) the corresponding trucks in any optimal solution:
      **Base case**: Suppose our first truck packs boxes 1 through $r_1$. If the base station in the optimal solution goes beyond $r_1$, then the first truck must also include box $r_1+1$. However $r_1+1$ does not fit in our first truck's capacity, so it must also exceed the capacity in the optimal solution. Therefore our solution is not behind compare to other solution.
      **Inductive step**: Assume our kth truck is as far along as the kth truck in any optimal solution (i.e., it includes at least as many boxes). Now look at the $(k+1)^{st}$ truck. In our solution, we start packing right after truck k finished, up to the point where adding another box would exceed capacity. If any optimal solution’s $(k+1)^{st}$ truck included more boxes, it would also exceed capacity (for the same reason as above). Thus our $(k+1)^{st}$ truck is also not behind any optimal solution’s $(k+1)^{st}$ truck.
   
   2. Now assume our solution required m trucks, and there is an optimal solution with fewer than m trucks. We now look at our last truck, which starts exactly where our $(m-1)^{st}$ truck could not fit another box. If any other solution also had fewer than n trucks, it would have to fit this “leftover” box into the $(m-1)^{st}$ truck, which by our induction argument also cannot hold it. This is a contradiction. Hence no solution can use fewer than m trucks.
   
   If there are n boxes, we simply make one pass over them. For each box, we either place it in the current truck or start a new truck if it doesn’t fit. Hence the time complexity is $O(n)$ once the boxes are given in arrival order.
   
   

2. Suppose you want to drive from USC to Santa Monica. Your gas tank, when full, holds enough gas to drive $p$ miles. Suppose there are $n$ gas stations along the route at distances $d_1 ≤ d_2 ≤ ... ≤ d_n$ from USC. Assume that the distance between any neighboring gas stations, and the distance between USC and the first gas station, as well as the distance between the last gas station and Santa Monica, are all at most $p$ miles. Assume you start from USC with the tank full. Your goal is to make as few gas stops as possible along the way. Design an efficient algorithm for determining the minimum number of gas stations you must stop at to drive from USC to Santa Monica. Prove that your algorithm is correct. Analyze the time complexity of your algorithm.

   **Solution:**
   Start driving from USC with a full gas tank and travel as far as possible. Whenever you cannot reach the next station or Santa Monica with your remaining fuel, stop at the station (among all the ones you have already passed) that gives you the farthest possible range when you refill. Continue this process of stopping and refilling until you reach Santa Monica.

   **Proof:**
   The proof is similar to that for the interval scheduling solution we did in lecture. We will show, by using mathematical induction and contradiction, that our greedy choice of stopping at the last possible station before running out of gas leads to the minimum number of stops.

   1. Our stops are always as far along as (or not behind) the corresponding stops in any optimal solution

      **Base Case:** Our first potential stop is at the farthest station we can reach from USC on a full tank. If there were an optimal solution that stopped earlier, that would mean it wastes some remaining fuel capacity. By our greedy rule, we do not stop until absolutely necessary—therefore, our first stop is at least as far along as any optimal solution’s first stop.

      **Inductive Step:** Assume for the $k$th stop that we are at least as far along as the $k$th stop of any optimal solution. Now, from that stop, we drive again until we cannot reach the next station (or Santa Monica). If an optimal solution stops at a station farther along for the $(k+1)^{st}$ stop, then our greedy solution would also have been able to reach that station without refueling earlier. Hence, by not stopping sooner, we also ensure the $(k+1)^{st}$ stop is as far along as (or not behind) the optimal solution’s $(k+1)^{st}$ stop.

   2. Now assume that our greedy strategy requires $m$ stops, but there exists an alternative solution with fewer than $m$ stops. By the induction above, each of our stops matches or surpasses the position of the corresponding stop in any other solution. This means we never waste a potential stretch of fuel between stops. If another solution claimed to use fewer stops, it would mean it skips refueling at a time when we found it necessary. However, we have shown that if we needed to stop, no better solution could have made it any farther without refueling. This is a contradiction. Thus, our greedy algorithm is optimal and uses the minimum number of stops.

   We can implement the greedy approach in a single pass over the station list, checking how far we can get with the current fuel. Thus, the time complexity is **$$O(n)$$**.

   

3. There are N tasks that need to be completed using 2 computers A and B. Each task $i$ has 2 parts that take time: $ai$ (first part) and $bi$ (second part) to be completed. The first part must be completed before starting the second part. Computer A does the first part of all the tasks while computer B does the second part of all the tasks. Computer A can only do one task at a time, while computer B can do any amount of tasks at the same time. Find an $O(n log n)$ algorithm that minimizes the time to complete all the tasks, and give a proof of why the solution obtained by the algorithm is optimal. (15 points)

   **Solution:**

   Find the task with the largest second-part time ($b_i$) among all tasks and schedule its first part on Computer A first. Remove that task from the list of unscheduled tasks, then find the next largest second-part time from the remaining tasks and schedule the task's first part next on Computer A. Continue this process until all tasks are scheduled on Computer A in a decreasing order of their $b_i$ values. As soon as a task finishes on Computer A, immediately starts its second part on Computer B (which can handle multiple tasks concurrently).

   **Proof**:

   The proof is similar to that for the interval scheduling solution we did in lecture. We first show (using mathematical induction) that no schedule can do better by violating this “largest $b_i$ first” order. We then using proof by contradiction to show that our solution must therefore be optimal.

   1. Our scheduled tasks are always "as far along" (or not behind) compared to any optimal schedule:

      **Base case**: Suppose we have two tasks in our schedule, Task 1 and Task 2, with second-part times $(b_1, b_2)$ and we scheduled Task 1 before Task 2 (so $(b_1 \ge b_2)$). If an optimal schedule placed a “larger” second-part time after a “smaller” one (i.e., $(b_1 < b_2)$ in that order), we could swap them without increasing the total finishing time. Hence placing the task with the larger $b_i$ first is never worse.

      **Inductive step**: Assume for the first $k$ tasks, any other schedule that tries to reorder them cannot finish earlier. Now look at the $(k+1)^{th}$ task in our schedule. If in some other schedule this task (with larger $b_i$) appears after a task with a smaller $b_j$​, then by our base case swapping argument, we can swap them without making the finish time worse. Repeating this argument shows that our schedule (which keeps tasks in decreasing order of $b_i$) is always at least as early as any other schedule.

   2. Now assume our solution finishes in time $T$, but there exists another solution that finishes in time less than $T$. If their ordering of tasks does not match our algorithm (sorted by decreasing $b_i$), then there must be a pair of tasks out of order. By the induction argument above, swapping them will not increase the finishing time, implying that we could reorder the schedule to match our method without ending any later. This contradicts the assumption that some solution significantly improves on ours. Therefore, no schedule can have a strictly better (smaller) finishing time than ours.

   Since sorting the tasks in decreasing order of $b_i$ takes $O(n \log n)$ time and scheduling them in that order requires just one pass through the list $O(n)$, the total running time of our algorithm is $O(n\log n) $

   

4. (a) Consider the problem of making change for n cents using the fewest number of coins. Describe a greedy algorithm to make change consisting of quarters (25 cents), dimes (10 cents), nickels (5 cents) and pennies (1 cents). Prove that your algorithm yields an optimal solution. (Hints: consider how many pennies, nickels, dimes and dime plus nickels are taken by an optimal solution at most.)
   (b) For the previous problem, give a set of coin denominations for which the greedy algorithm does not yield an optimal solution. Assume that each coin’s value is an integer. Your set should include a penny so that there is a solution for every value of n. (15 points)

   **Answer:**

   (a) **Solution:**

   Take as many quarters (25 cents) as possible without exceeding the amount. Next, take as many dimes (10 cents) as possible from the remainder. Then, take as many nickels (5 cents) as possible from what is left. Finally, use pennies (1 cent) for the leftover amount. This algorithm stops once the total amount is reduced to 0.

   **Proof:**

   The proof is similar to that for the interval scheduling solution we did in lecture. We first show (using mathmatical induction) that the greedy use of quarters, dimes, nickels, and pennies is always "as good as" (or not worse than) any other solution. Using this fact, we can then show that our solution is optimal (using a proof by contradiction).

   1. Our coin choice is always as far along as (or not behind) the corresponding choice in any optimal solution:

      **Base Case (quarters)**: Suppose an optimal solution used fewer quarters than our greedy method. Then it must use more dimes/nickels/pennies to make up the same total of cents, which only increases the number of coins. Hence our use of quarters does not lag behind any optimal solution.

      **Inductive Step (dimes, nickels, pennies):** After taking the maximum possible quarters, we apply the same logic with dimes; if an optimal solution took fewer dimes than we did, it would have to use more nickels/pennies to make the same amount. Similarly for nickels: if an optimal solution didn’t use a nickel where possible, it would have to use extra pennies. In each case, that would not reduce—and would typically increase—the total coin count.

   2. Now assume our solution used k coins, and there is an optimal solution with fewer than k coins. Since we argued above that our greedy steps never fall behind, the only way to use fewer coins would be to replace one of our “larger” coins (quarters/dimes/nickels) with several smaller ones in some cunning way. But we see from arithmetic (25 cents cannot be replaced by 2 dimes plus 1 nickel plus pennies and still use fewer coins, etc.) that no such improvement is possible. This is a contradiction. Therefore, no solution can use fewer than k coins.

   Hence, making change by taking the largest U.S. coin that fits at each step is optimal.

   (b) Suppose the set of coin denominations is {1, 3, 4}. When making change for 6 cents, the greedy approach would first pick a 4-cent coin and then two 1-cent coins, for a total of 3 coins. However, the optimal solution would be to use two 3-cent coins, requiring only 2 coins. Since the greedy solution uses 3 coins while the optimal solution uses only 2, the greedy approach does not yield an optimal solution.