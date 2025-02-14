# CSCI 570 Spring 2025 Homework 4

1. [10 points] Design a data structure that has the following properties (assume n elements in the data structure, and that the data structure properties need to be preserved at the end of each operation):

   - Find median takes O(1) time

   - Insert takes O(log n) time

   Do the following: 

   1. Describe how your data structure will work. 
   2. Give algorithms that implement the Find-Median() and Insert() functions.

   **Answer**:

   1. Data Structure Description

      We can maintain two heaps: A max-heap called `lowers` to store the smaller half of the numbers, and a min-heap called `highers` to store the larger half of the numbers. 

      The two heaps differ in size by at most 1. If the total number of elements is odd, one heap will have one extra element, and that root represents the median. Else if the total number of elements is even, the median is the average of the two roots.

   2. Algorithms

      Find-Median()

      ```pseudocode
      function FindMedian(): 
      	if size(lowers) > size(highers): 
      		return top(lowers) 			// root of max-heap 
          else if size(lowers) < size(highers): 
              return top(highers) 		// root of min-heap 
          else: 
          	return (top(lowers) + top(highers)) / 2
      ```

      Insert(x)

      ```pseudocode
      function Insert(x): 
      	// Decide which heap to insert into 
      	if lowers is empty OR x <= top(lowers): 
      		push x into lowers 		// max-heap 
          else: 
          	push x into highers 	// min-heap
          
          // Rebalance if size difference is more than 1
      	if size(lowers) - size(highers) > 1:
      		temp = pop(lowers)
      		push temp into highers
          else if size(highers) - size(lowers) > 1:
          	temp = pop(highers)
          	push temp into lowers
      ```

      

2. [10 points] In a busy grocery store, there are k self-checkout lanes, each with customers waiting in line. The store organizes these lanes so that within each line, customers are arranged in increasing order of their time of arrival—nobody skips ahead, and everyone follows the rules. The store manager wants to merge all k lines into a single checkout queue, ensuring that customers are still ordered by their arrival time. However, since the store is crowded, they need to do this as efficiently as possible. How can the manager merge these k sorted lines into one single sorted line in the fastest possible way, ensuring an optimal time complexity of O(n log k), where n is the total number of customers across all lines? Can you describe an algorithm that achieves this, justify its correctness, and explain why it runs in O(n log k) time?

   **Answer:**

   Algorithm:

   1. Initialize a min-heap (priority queue) with size up to $$k$$.
   2. Insert the first customer from each of the $$k$$ lines (their arrival times and line IDs) into the min-heap.
   3. While the min-heap is not empty:
      - Extract the minimum element (the customer with the earliest arrival time).
      
      - Append that customer to the merged queue.
      - From the line that this customer came from, insert the next customer (if any) into the min-heap.
   
   Correctness:
   - Each insertion in the min-heap maintains that the root is always the earliest arrival among all front-line customers. 
   - By repeatedly extracting the min, we guarantee an overall sorted (by arrival time) merged queue.
   
   Time Complexity:
   - Let $$n$$ be the total number of customers, and $$k$$ be the number of lines.
   - Each customer is pushed and popped from the min-heap exactly once, incurring a cost of $$O(\log k)$$ for each operation.
   - Therefore, the total time is $$O(n \log k)$$.



3. [5 points] A town wants to build roads connecting all neighborhoods at the lowest total cost, with each road having a unique construction cost. The mayor needs to know: Can there be more than one way to build this minimum-cost road network, or is the solution always unique? Prove why the answer must be yes or no.

   **Answer:** The minimum-cost road network (or minimum spanning tree, MST) is always unique when all road construction costs are distinct.

   **Proof:**

   1. **Assume for contradiction** that there are two different MSTs, call them $$T$$ and $$T'$$.

   2. **Consider the symmetric difference** $$T \oplus T'$$ (the set of roads that are in one tree but not the other). Since $$T$$ and $$T'$$ are different, $$T \oplus T'$$ is non-empty.

   3. **Let $$e$$ be the road (edge) in $$T \oplus T'$$ with the smallest construction cost.** Without loss of generality, assume $$e$$ is in $$T$$ but not in $$T'$$.

   4. **Adding $$e$$ to $$T'$$ creates a cycle.** In this cycle, there must be at least one road $$f$$ that is in $$T'$$ but not in $$T$$.

   5. **Because road costs are unique,** the cost of $$e$$ is strictly less than the cost of $$f$$ (by the minimality of $$e$$ in the symmetric difference).

   6. **Replace $$f$$ with $$e$$ in $$T'$$:** This gives a new spanning tree $$T''$$ with a lower total cost than $$T'$$ (since $$e$$ is cheaper than $$f$$). This contradicts the assumption that $$T'$$ was a minimum spanning tree.

   7. **Conclusion:** Our assumption that two different MSTs exist must be false. Therefore, when all road (edge) costs are unique, the MST is unique.

   Thus, the mayor can be assured that there is only one way to build the minimum-cost road network.



4. [10 points] Suppose you are given a connected undirected graph where every edge weight is either 1 or 2. You want to find an MST. 
   - Show that Prim’s algorithm will always find an MST in O(n log n) time for this graph.
   - Can we do beer than O(n log n)? Justify your answer—if yes, provide an algorithm with its time complexity; if no, give a proof

   ### Part 1: Prim’s Algorithm in O(n log n) Time

   Even if we use a standard binary heap as our priority queue, Prim’s algorithm will correctly compute the MST. Here’s why:

   1. **Correctness:**  
      Prim’s algorithm grows a tree by repeatedly adding the minimum-weight edge that connects a vertex not yet in the tree. This greedy method is known to always produce an MST for any connected weighted graph.

   2. **Time Complexity with a Binary Heap:**  
      - There are $$n$$ vertices.  
      - Each vertex is inserted into the heap and extracted exactly once, with each extract-min costing $$O(\log n)$$.  
      - Although there are also update (decrease-key) operations for the neighbors of the extracted vertices, in the worst case they add extra $$O(\log n)$$ time per operation.  
      - Thus, the overall running time is bounded by $$O(n \log n + \text{(updates)})$$.  
        
      
      In many cases (especially if the graph is sparse or if we only have $$O(n)$$ effective update operations because the keys come only from a very small set), this leads to an overall time of $$O(n \log n)$$.

   ### Part 2: Can We Do Better than O(n log n)?

   Yes, we can do better than $$O(n \log n)$$ for this special case where every edge weight is either 1 or 2. Here are two approaches:

   #### 1. **Bucket-Based Prim’s Algorithm (or Dial’s Algorithm Style):**

   - **Observation:**  
     In Prim’s algorithm, the key for each vertex is the weight of the lightest edge connecting it to the current tree. Since all edge weights are 1 or 2 (and the starting vertex has key 0), the possible key values are only $$0, 1,$$ or $$2$$.

   - **Implementation:**  
     Instead of using a binary heap, we can maintain three buckets (or lists), one for each possible key value.  
     - **Bucket 0:** Initially contains the starting vertex.  
     - **Buckets 1 and 2:** Will hold vertices that become adjacent with edge weights 1 or 2, respectively.  
     - When extracting a vertex, we simply choose the first nonempty bucket (starting with bucket 0, then 1, then 2).  
     - Updating a vertex’s key means moving it from one bucket to another; each such update takes constant time.

   - **Time Complexity:**  
     Since every vertex is processed in constant time per bucket operation and each edge is inspected once, the overall time is $$O(n + m)$$. For a connected graph (with $$m \ge n-1$$), this is linear in the size of the input, which is much better than $$O(n \log n)$$ when the graph is sparse.

   #### 2. **Kruskal’s Algorithm with Counting Sort:**

   - **Observation:**  
     The only two edge weights are 1 and 2. This means we can sort the edges in $$O(m)$$ time using counting sort (or bucket sort), rather than $$O(m \log m)$$ time.

   - **Implementation:**  
     - Partition the edges into two groups based on their weight (1 or 2).  
     - Process the edges in increasing order (all weight 1 edges first, then weight 2).  
     - Use a union-find (disjoint set) data structure to decide whether to add an edge to the MST.

   - **Time Complexity:**  
     Sorting takes $$O(m)$$ time, and the union-find operations take nearly linear time (amortized $$O(m \alpha(n))$$, where $$\alpha$$ is the inverse Ackermann function). Hence, the overall complexity is $$O(m)$$, which is optimal for sparse graphs.

   ### **Summary Answer:**

   - **Prim’s Algorithm:**  
     With a standard binary heap, it runs in $$O(n \log n)$$ time. However, due to the restricted set of edge weights, a bucket-based implementation yields an improved time of $$O(n + m)$$.

   - **Better than $$O(n \log n)$$:**  
     Yes, we can. Either by using a bucket-based version of Prim’s algorithm or by using Kruskal’s algorithm with counting sort (and union-find), we can achieve an overall running time of $$O(n + m)$$. For sparse graphs (where $$m = O(n)$$), this is linear, which is better than $$O(n \log n)$$.

5. [5 points] Design an algorithm to find the maximum bandwidth path between a given source vertex s and a destination vertex t in a weighted graph G = (V, E), where each edge weight represents bandwidth capacity. The bandwidth of a path is defined as the minimum edge weight along that path (i.e., the bottleneck). Explain how to modify Dijkstra’s algorithm to do this.

   Answer:

   We can solve the maximum bandwidth path (also known as the widest path) problem by modifying Dijkstra’s algorithm. Instead of trying to minimize the total distance (sum of edge weights), we want to maximize the bandwidth of a path, which is defined as the minimum edge weight (the bottleneck) along that path.

   ### Modified Dijkstra’s Algorithm for Maximum Bandwidth Path

   1. **Initialization:**

      - For each vertex $$v \in V$$, let $$B(v)$$ be the maximum bandwidth from the source $$s$$ to $$v$$ found so far.
      - Set $$B(s) = \infty$$ (or a value larger than any edge weight) since there is no bottleneck at the source.
      - For all other vertices, initialize $$B(v) = 0$$.
      - Use a max-priority queue $$Q$$ keyed by $$B(v)$$. (We want to always choose the vertex with the highest current bandwidth value.)

   2. **Relaxation Rule:**

      - When exploring an edge $$(u,v)$$ with weight $$w(u,v)$$, the potential bandwidth for $$v$$ via $$u$$ is given by
        $$$
        candidate = \min\{B(u), w(u,v)\}.
        $$$
      - If $$candidate > B(v)$$, update:
        $$$
        B(v) \gets candidate \quad \text{and} \quad parent(v) \gets u.
        $$$
        
        Also, update the position of $$v$$ in the max-priority queue (using an increase-key operation).

   3. **Algorithm:**

      ```pseudocode
      function MaximumBandwidthPath(G, s, t):
          for each vertex v in V:
              B(v) = 0
              parent(v) = NIL
          B(s) = ∞
      
          Initialize a max-priority queue Q with all vertices keyed by B(v)
      
          while Q is not empty:
              u = extract_max(Q)
              if u == t:
                  break  // We can stop once we extract t, as its bandwidth is finalized.
              for each edge (u, v) in E:
                  candidate = min(B(u), w(u, v))
                  if candidate > B(v):
                      B(v) = candidate
                      parent(v) = u
                      increase_key(Q, v, B(v))
      
          return B(t), parent  // B(t) is the maximum bandwidth from s to t, and parent[] can be used to reconstruct the path.

1. **Explanation:**
   - **Selection:**
     In each iteration, we select the vertex uuu with the highest current bandwidth B(u)B(u)B(u). This is analogous to choosing the vertex with the smallest tentative distance in standard Dijkstra, but here we want to preserve as much bandwidth as possible.
   - **Relaxation:**
     When relaxing an edge (u,v)(u, v)(u,v), we calculate the candidate bandwidth for vvv by taking the minimum of the bandwidth up to uuu and the capacity w(u,v)w(u,v)w(u,v) of the edge. This reflects the fact that the bottleneck along a path is the smallest capacity edge.
   - **Correctness:**
     Much like Dijkstra’s algorithm, the greedy selection is correct here because once a vertex is extracted from the queue, the maximum possible bandwidth from sss to that vertex has been determined.
2. **Time Complexity:**
   - With a standard binary heap, each extract-max operation takes O(log⁡∣V∣)O(\log |V|)O(log∣V∣) time, and each edge relaxation (with an update/increase-key) takes O(log⁡∣V∣)O(\log |V|)O(log∣V∣) time.
   - Thus, the overall running time is similar to Dijkstra's algorithm, i.e., O(∣E∣log⁡∣V∣)O(|E| \log |V|)O(∣E∣log∣V∣).

### Summary

By modifying the relaxation step to use the minimum of the current path bandwidth and the edge weight, and by using a max-priority queue to select the vertex with the maximum bandwidth so far, we can find the maximum bandwidth path from sss to ttt in a graph. This modified algorithm is essentially Dijkstra’s algorithm adapted for the bottleneck (widest path) optimization problem.
