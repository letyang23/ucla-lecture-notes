# CSCI 570 Spring 2025 Homework 4

1. [10 points] Design a data structure that has the following properties (assume n elements in the data structure, and that the data structure properties need to be preserved at the end of each operation):

   - Find median takes O(1) time

   - Insert takes O(log n) time

   Do the following: 

   1. Describe how your data structure will work. 
   2. Give algorithms that implement the Find-Median() and Insert() functions.

   **Answer**:

   1. Data Structure Description

      We can maintain two heaps: A **max-heap** (`lowers`) to store the smaller half of the numbers, and a **min-heap** (`highers`) to store the larger half of the numbers. 

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



4. [10 points] Suppose you are given a connected undirected graph where every edge weight is either 1 or 2. You want to find an MST. 
   - Show that Prim’s algorithm will always find an MST in O(n log n) time for this graph.
   - Can we do beer than O(n log n)? Justify your answer—if yes, provide an algorithm with its time complexity; if no, give a proof



5. [5 points] Design an algorithm to find the maximum bandwidth path between a given source vertex s and a destination vertex t in a weighted graph G = (V, E), where each edge weight represents bandwidth capacity. The bandwidth of a path is defined as the minimum edge weight along that path (i.e., the bottleneck). Explain how to modify Dijkstra’s algorithm to do this.

