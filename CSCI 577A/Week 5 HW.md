# Chapter 9 End-of-Chapter Assignments

Assignment 2 Using Voas & Kuhn (2017) insights cited in the chapter, derive a modern set of rules for metric selection and explain why single-metric programs fail.

**Answer:**

Single-metric programs fail because they measure only one dimension of software complexity, creating severe analytical blind spots. For instance, relying exclusively on Halstead Complexity Metrics provides a purely lexical assessment based on counting operators and operands, but it completely ignores structural complexity. Because of this, two programs with identical token counts but vastly different control flows—such as one being highly linear and the other containing complex nested loops—would yield the exact same complexity score. Additionally, single metrics often oversimplify cognitive load; Halstead treats a simple assignment operator exactly the same as a complex mathematical function call, which misrepresents the actual human effort required to understand and maintain the code.

To prevent these failures, metric selection must adhere to a multidimensional approach. The primary rule is to mandate orthogonal coverage by pairing lexical metrics with structural ones. For example, an organization should combine Halstead metrics to understand a program's vocabulary and operational density alongside McCabe's Cyclomatic Complexity to evaluate its logical branching and decision points. Furthermore, metric selection must be phase-appropriate. Teams should use functional metrics like Function Points for early project estimation based on user requirements, and reserve code-level metrics like Halstead's Program Volume ($V = N \times \log_2 n$) for quantitative assessment only after the source code is actively implemented.



# Chapter 10 End-of-Chapter Assignments

Assignment 1 Explain Cyclomatic Complexity using Control Flow Graphs. Reproduce McCabe’s formula and explain the meaning of each variable exactly as described in the chapter.

**Answer:**

Cyclomatic Complexity is analyzed using a Control Flow Graph (CFG), which is a directed graph that visually models all possible execution paths of a program. The CFG consists of Nodes representing basic blocks of code (sequences with a single entry and exit point), Edges representing the transfer of control between these basic blocks, and Connected Components representing reachable parts of the program. To calculate this structural complexity, McCabe established the following formula:

$$M = E - N + 2P$$

In this formula, exactly as described in the chapter, $M$ represents the Cyclomatic Complexity, $E$ represents the number of edges in the Control Flow Graph, $N$ represents the number of nodes in the Control Flow Graph, and $P$ represents the number of connected components (which is usually 1 for a single program or function).



###### AI Usage Disclosure 

In the completion of this assignment, I used AI tool (Google Gemini) to help in synthesizing the provided course readings and structuring the final responses.
