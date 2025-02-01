# CSCI 570 Spring 2025 Homework 2

1. What is the tight upper bound to the worst-case runtime performance of the procedure below? (8 points)

   ```pseudocode
   c = 0
   i = n
   while i > 1 do
   	for j = 1 to i do
   		c = c + 1
   	end for
   	i = floor(i/2)
   end while
   return c
   ```

   **Answer:**

   The tight upper bound to the worst-case runtime is $$\Theta(n)$$. This is because the outer while loop runs approximately $$\log_2 n$$ times, and in each iteration, the inner for loop executes $$i$$ times where $$i$$ starts at $$n$$ and is halved each time. The total work done is:

   $$
   n + \frac{n}{2} + \frac{n}{4} + \cdots \approx 2n,
   $$

   which simplifies to an overall time complexity of $$\Theta(n)$$.

   

2. Given functions $f_1$, $f_2$, $g_1$, $g_2$ such that $f_1(n) = O(g_1(n))$ and $f_2(n) = O(g_2(n))$. For each of the following statements, decide whether you think it is true or false and give a proof or counterexample. (12 points)

   (a) $f_1(n) \cdot f_2(n) = O(g_1(n) \cdot g_2(n))$

   (b) $f_1(n) + f_2(n) = O(\max(g_1(n), g_2(n)))$

   (c) $f_1(n)^2 = O(g_1(n)^2)$

   (d) $\log_2 f_1(n) = O(\log_2 g_1(n))$

   **Answer:**

   **(a) True.**

   Since 
   $$
   f_1(n) = O(g_1(n)) \quad \text{and} \quad f_2(n) = O(g_2(n)),
   $$
   there exist constants $$c_1, c_2 > 0$$ and $$n_0$$ such that for all $$n \ge n_0$$,
   $$
   f_1(n) \le c_1 \, g_1(n) \quad \text{and} \quad f_2(n) \le c_2 \, g_2(n).
   $$
   If we multiplying these inequalities, we gets
   $$
   f_1(n) \cdot f_2(n) \le (c_1 c_2) \, (g_1(n) \cdot g_2(n)),
   $$
   so
   $$
   f_1(n) \cdot f_2(n) = O(g_1(n) \cdot g_2(n)).
   $$

   ---

   **(b) True.**

   From the assumptions,
   $$
   f_1(n) \le c_1 \, g_1(n) \quad \text{and} \quad f_2(n) \le c_2 \, g_2(n).
   $$
   Thus,
   $$
   f_1(n) + f_2(n) \le c_1 \, g_1(n) + c_2 \, g_2(n).
   $$
   For any nonnegative functions,
   $$
   g_1(n) + g_2(n) \le 2 \cdot \max(g_1(n), g_2(n)).
   $$
   Therefore,
   $$
   f_1(n) + f_2(n) \le (c_1 + c_2) \cdot \max(g_1(n), g_2(n)) \quad \Rightarrow \quad f_1(n) + f_2(n) = O(\max(g_1(n), g_2(n))).
   $$

   ---

   **(c) True.**

   Since
   $$
   f_1(n) \le c_1 \, g_1(n),
   $$
   squaring both sides gives
   $$
   f_1(n)^2 \le c_1^2 \, g_1(n)^2,
   $$
   which means
   $$
   f_1(n)^2 = O(g_1(n)^2).
   $$

   ---

   **(d) False.**

   Consider the counterexample where 
   $$
   f_1(n)=\frac{1}{n} \quad \text{and} \quad g_1(n)=1.
   $$
   since for all $$n \ge 1$$,
   $$
   \frac{1}{n} \le 1,
   $$
   so 
   $$
   f_1(n)=O(g_1(n)).
   $$

   Now, look at the logarithms:
   - We have
     $$
     \log_2 f_1(n)=\log_2\left(\frac{1}{n}\right)=-\log_2 n,
     $$
   - and
     $$
     \log_2 g_1(n)=\log_2 1=0.
     $$

   Since $$-\log_2 n$$ (in absolute value, $$\log_2 n$$) grows without bound as $$n$$ increases, there is no constant $$c$$ such that
   $$
   |\log_2 f_1(n)| \le c \cdot |\log_2 g_1(n)|
   $$
   for large $$n$$ because the right-hand side is always zero. Thus,
   $$
   \log_2 f_1(n) \neq O(\log_2 g_1(n)).
   $$

   ---

   In conclusion,  (a), (b), (c) are **true** and (d) is **false**.



3. Given an undirected graph G with n nodes and m edges, design an O(m+n) algorithm to detect whether G contains a cycle. Your algorithm should output a cycle if G contains one. (10points)

   **Answer:**

   We can detect a cycle in an undirected graph in $$O(m+n)$$ time using DFS approach. The idea is to traverse the graph while keeping track of visited vertices and the parent vertex in the DFS tree. If during the DFS we encounter a vertex that has already been visited and is not the parent of the current vertex, then a cycle exists.

   ```pseudocode
   function findCycle(G):
       for each vertex v in G:
           visited[v] = false
           parent[v] = -1
       for each vertex u in G:
           if visited[u] == false:
               cycle = DFS(u, -1)
               if cycle != null:
                   return cycle
       return null
   
   function DFS(v, p):
       visited[v] = true
       parent[v] = p
   
       for each neighbor w in adjacencyList[v]:
           if visited[w] == false:
               cycle = DFS(w, v)
               if cycle != null:
                   return cycle
           else if w != p:
               cycle = []
               x = v
               cycle.append(x)
               while x != w:
                   x = parent[x]
                   cycle.append(x)
               cycle.append(v) 
               return cycle
       return null
   ```

   The DFS visits each vertex and examines each edge at most once, leading to an overall time complexity of $$O(m+n)$$.

   

4. Design an algorithm which, given a directed graph $G = (V, E)$ and a particular edge $e \in E$ going from node u to node v, determines whether G has a cycle containing e. The running time should be bounded by $O(|V | + |E|)$. Explain why your algorithm runs in $O(|V | + |E|)$ time. (10points)

   **Answer:**

   Given a directed graph $$G=(V,E)$$ and a specific edge $$e = (u,v)$$, we can determine whether there is a cycle that contains $$e$$ by checking if there is a path from $$v$$ back to $$u$$ in the graph after temporarily removing $$e$$. If such a path exists, then including $$e$$ forms a cycle. 

   **Pseudocode:**

   ```pseudocode
   function hasCycleContainingEdge(G, e): 
       // Temporarily remove edge e from G
       Remove e from G
   
       // Check if u is reachable from v using DFS
       if DFS(G, v, u) returns True:
           return True   // A path from v to u exists, so a cycle containing e exists
       else:
           return False
   
   function DFS(G, current, target):
       if current == target: 
           return True
       mark current as visited
       for each neighbor w of current in G:
           if w is not visited:
               if DFS(G, w, target) returns True:
                   return True
       return False
   ```

   The DFS traversal visits each vertex and edge at most once, which takes $$O(|V| + |E|)$$ time. Removing or ignoring the single edge $$e$$ is a constant-time operation. Thus, the overall algorithm runs in $$O(|V| + |E|)$$ time.

   

5. For each of the following, indicate if $f = O(g)$, $f = \Theta(g)$, or $f = \Omega(g)$. (10 points)

   1. $f(n) = \frac{n^4}{\log(n)}$, $g(n) = n(\log(n))^4$


   2. $f(n) = n \cdot \log(n)$, $g(n) = n^2 \log(n^2)$
   3. $f(n) = \log(n)$, $g(n) = \log(\log(5^n))$
   4. $f(n) = n^{1/3}$, $g(n) = (\log(n))^3$
   5. $f(n) = 2^n$, $g(n) = 2^{3n}$

​	

**Answer**:

1. $$f(n) = \frac{n^4}{\log(n)}, \quad g(n) = n(\log(n))^4$$  

   - For the ratio:
     $$
       \frac{f(n)}{g(n)} = \frac{\tfrac{n^4}{\log(n)}}{n(\log(n))^4}
       = \frac{n^4}{\log(n)} \cdot \frac{1}{n(\log(n))^4}
       = \frac{n^3}{(\log(n))^5}.
     $$
     As $$n \to \infty$$, $$n^3$$ will grow faster than $$(\log(n))^5$$. Therefore, $$f(n)$$ grows at least as fast as $$g(n)$$, i.e., $$f = \Omega(g).$$

   - **Answer**: $$f = \Omega(g)$$

2. $$f(n) = n \log(n), \quad g(n) = n^2 \log(n^2)$$  

   - Since $$\log(n^2) = 2 \log(n).$$ Thus:
     $$
       g(n) = n^2 \cdot 2 \log(n) = 2n^2 \log(n).
     $$
     The ratio:
     $$
       \frac{f(n)}{g(n)} = \frac{n \log(n)}{2n^2 \log(n)} = \frac{1}{2n}.
     $$
     This ratio goes to 0 as $$n \to \infty$$. Therefore $$f(n)$$ is asymptotically smaller, so $$f = O(g).$$

   - **Answer**: $$f = O(g)$$

3. $$f(n) = \log(n), \quad g(n) = \log\bigl(\log(5^n)\bigr)$$  

   - Since $$\log(5^n) = n \log(5).$$ Then:
     $$
       g(n) = \log\bigl(n \log(5)\bigr)
             = \log(n) + \log(\log(5)),
     $$
     which is asymptotically like $$\log(n)$$ for large $$n$$. Hence $$f(n)$$ and $$g(n)$$ grow at the same rate, giving $$f = \Theta(g).$$

   - **Answer**: $$f = \Theta(g)$$

4. $$f(n) = n^{1/3}, \quad g(n) = (\log(n))^3$$  

   - Polynomial functions eventually outgrow logarithmic functions. Thus $$f(n)$$ grows faster, so $$f = \Omega(g).$$

   - **Answer**: $$f = \Omega(g)$$

5. $$f(n) = 2^n, \quad g(n) = 2^{3n}$$  

   - Since $$2^{3n} = (2^n)^3.$$ $$2^{3n}$$ grows much faster than $$2^n.$$ so $$f = O(g).$$

   - **Answer**: $$f = O(g)$$
