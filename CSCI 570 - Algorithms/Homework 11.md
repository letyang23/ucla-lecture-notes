# CSCI 570 Spring 2025 Homework 11

1. (14 points) Consider the problem Spanning Tree with Bounded Degree (STBD): Given an undirected graph G = (V, E) and integer k > 0, determine whether there is a spanning tree where the maximum vertex degree in the tree is not greater than k, i.e, each vertex has at most k neighbors within the tree, but may have other neighbors in G overall. Prove that STBD is NP-complete.

  ###### Answer:

  1. We first going to prove STBD is in NP. 

     If someone hands you a candidate tree, you can verify in linear time that

     - it has $|V|-1$ edges and is connected (so it’s a tree), and
     - every vertex degree in that tree is $\le k$.

  2. STBD is NP-hard (even when $k=2$)

     - We can do the reduction on the known NP-complete problem Hamiltonian Path (HP).

       For an HP instance $G$, output the pair $(G,\,2)$. Since a Hamiltonian path is a spanning tree whose vertices all have degree $\le 2$. Conversely, any spanning tree of $G$ with max degree $\le 2$ must be a single path that visits every vertex once (i.e., a Hamiltonian path). Thus $G$ has a Hamiltonian path iff $(G,2)$ is a YES-instance of STBD.

  Because STBD is in NP and HP reduces to it in polynomial time, STBD is NP-complete.

  

2. (15 points) Given an undirected graph with positive edge weights, the BIG HAM CYCLE (BHC) problem is to decide if it contains a Hamiltonian cycle C such that the sum of weights of edges in C is at least half of the total sum of weights of edges in the graph. Show that BHC is NP-complete.

  ###### Answer:

  1. BHC is in NP: A certificate is simply a list of the $n$ edges that form the cycle.
      In $O(|E|)$ time we can verify the edges visit every vertex once (Hamiltonian), and add their weights and compare with $\frac12\!\sum_{e\in E}w(e)$.

  2. Reduction from Hamiltonian Cycle:

     - To reduce Hamiltonian Cycle (HC) to BIG HAM CYCLE (BHC), start with an undirected graph $G=(V,E)$ that constitutes the HC instance.  Construct a new graph $G'=(V,E')$ on the same vertex set but make it complete: keep every original edge and insert all missing edges so that $E'=\binom{V}{2}$.  Assign weights in a “heavy vs. light’’ style.  Give each edge that already belonged to $E$ a large weight $M = 2|E| + 1$; give every newly added edge weight $1$.  Because $G'$ is complete, any Hamiltonian cycle is possible, but its total weight depends on whether it uses only heavy edges or at least one light edge.  Let $H$ denote the set of heavy edges ($|H|=|E|$) and $L$ the set of light edges, and let $S = |H|M + |L|$ be the sum of all edge-weights in $G'$; the BHC threshold is $S/2$.

       If the original graph $G$ contains a Hamiltonian cycle, the same $n$-edge cycle exists in $G'$ using only heavy edges.  Its weight is $nM$, which exceeds $S/2$ because $M$ dominates the overall total.  Conversely, if $G$ has no Hamiltonian cycle, then every Hamiltonian cycle in the complete graph $G'$ must include at least one light edge.  Any such cycle has weight at most $(n-1)M + 1$, which is strictly less than $S/2$.  Hence $G'$ meets the BHC criterion precisely when $G$ was a YES-instance of HC.  The transformation clearly runs in time polynomial in the size of $G$, so it is a valid many-one reduction.  Together with the fact that BHC lies in NP (its certificate can be checked in polynomial time), this establishes that BHC is NP-complete.

 



3. (15 points) In the Bipartite Directed Hamiltonian Cycle (BDHC) problem, we are given a directed graph G = (V, E) that is bipartite, i.e., V can be partitioned as $L \cup R$  s.t. each edge goes from 'L to R' or 'R to L', and we are asked whether there is a simple cycle which visits every vertex exactly once. It is known that the Directed Hamiltonian Cycle is an NP-complete problem. Prove that BDHC is NP-Complete as well.

  ###### Answer:

  1. BHDC in NP: 

     Given a candidate cycle for a bipartite digraph we can check, in linear time, that it visits every vertex once and that every used arc is present

  2. Reduction:

     For NP-hardness, take an arbitrary directed graph $G=(V,E)$ that forms an instance of DHC and turn it into a bipartite digraph $G'=(V',E')$ as follows.  Replace every vertex $v\in V$ by two new vertices $v^{\text{in}}$ and $v^{\text{out}}$; put all $v^{\text{in}}$ in the left part $L$ and all $v^{\text{out}}$ in the right part $R$.  Insert one private left-to-right arc $v^{\text{in}}\!\to v^{\text{out}}$ for each $v$.  For every original arc $u\!\to v$ in $E$, add a cross right-to-left arc $u^{\text{out}}\!\to v^{\text{in}}$.  The graph is now bipartite because every arc runs $L\to R$ or $R\to L$.

     The construction is polynomial and preserves Hamiltonicity:

     If $G$ has a Hamiltonian cycle $v_{1}\!\to v_{2}\!\to\dots\!\to v_{n}\!\to v_{1}$, then
      $v_{1}^{\text{in}}\!\to v_{1}^{\text{out}}\!\to v_{2}^{\text{in}}\!\to v_{2}^{\text{out}}\!\to\dots\!\to v_{n}^{\text{in}}\!\to v_{n}^{\text{out}}\!\to v_{1}^{\text{in}}$
      is a Hamiltonian cycle in $G'$ that alternates perfectly between $L$ and $R$.

     Conversely, any Hamiltonian cycle in $G'$ must enter a vertex $v^{\text{in}}$ from some $u^{\text{out}}$ and immediately continue along the mandatory arc $v^{\text{in}}\!\to v^{\text{out}}$; hence the cycle can be compressed to the sequence $u\!\to v\!\to\cdots$ of original vertices, yielding a Hamiltonian cycle of $G$.

     Thus $G$ has a directed Hamiltonian cycle iff $G'$ does, establishing a polynomial reduction DHC $\le_P$ BDHC.  Since DHC is NP-complete and BDHC is in NP, BDHC is NP-complete.





4. (16 points) Suppose we have a variation of the 3-SAT problem called Min-3-SAT, where the literals are never negated. Of course, in this case it is possible to satisfy all clauses by simply setting all variables to true. But, we are additionally given a number k, and are asked to determine whether we can satisfy all clauses while setting at most k variable to be true. Prove that Min-3-SAT is NP-Complete.

  ###### Answer:

  1. Min-3-SAT in NP: 

     a certificate consists of the assignment together with its list of at-most-$k$ variables set to true; in linear time we can check the assignment, count the true variables and confirm that every 3-literal (all-positive) clause is satisfied.

  2. Reduction:

     For NP-hardness we reduce Vertex Cover. Given a graph $G=(V,E)$ and an integer $k$, create a Boolean variable $x_v$ for every vertex $v\in V$. For every edge $e=\{u,v\}\in E$ introduce the length-three, monotone clause $(x_u \,\lor\, x_v \,\lor\, x_v),$ i.e. the edge endpoints, padding with one duplicate literal so the clause has exactly three literals and contains no negations. Let the resulting 3-CNF formula be $F$ and keep the same bound $k$.

     If $G$ has a vertex cover $C$ with $|C|\le k$, set $x_v=\text{true}$ for $v\in C$ and all other variables to false.  Every edge then has at least one endpoint in $C$, so its clause is satisfied; only $|C|\le k$ variables are true, hence $F$ is a YES-instance of Min-3-SAT.

     Conversely, if $F$ can be satisfied with at most $k$ variables set to true, pick the vertices whose variables are true; call this set $C$.  In each clause at least one of the two endpoints is true, therefore every edge is incident to a vertex in $C$; thus $C$ is a vertex cover of size $\le k$.

     This polynomial transformation shows Vertex Cover $\le_P$ Min-3-SAT, so Min-3-SAT is NP-hard.  Together with membership in NP, Min-3-SAT is NP-complete.
