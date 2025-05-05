1. Suppose you move to a new city. Due to busy work schedule, you have to eat out very often. There are m different food items that you are fond of. You seek recommendations from friends and online, and you get a list of n restaurants, each offering one or more (or none) of your m favorite foods. You realize this list is too big to try them all, so you want to remove as many from the list as possible while making sure that each of your favorite foods is offered in at least one of the remaining restaurants. Thus, the problem can be stated as deciding if at least k restaurants can be removed from the given list so that each of your favorite foods is offered in at least one of the remaining restaurants. Prove that the problem of shortening restaurant list (SRL) is

  a) in NP.

  b) NP-Hard using a poly-time reduction from Vertex Cover.

  ###### Answer:

a) NP: A candidate solution (subset of remaining restaurants) can be verified in polynomial time: check that all m foods are covered by the subset.

b) NP-Hard via Vertex Cover (VC) reduction:

- Map VC instance (graph $G = (V, E)$, target size $t$) to SRL:
  - Each vertex in $G$ → a restaurant.
  - Each edge in $G$ → a food item.
  - A restaurant "offers" a food (edge) if and only if the corresponding vertex is incident to the edge.
- Ask if $k = |V| - t$ restaurants can be removed (leaving $t$) to cover all foods.
- This is equivalent to finding a vertex cover of size $t$ in $G$.

Thus, SRL is NP-hard.

2. Given a graph G = (V, E) and a positive integer r, the dominating set problem (DSP) is to decide if there is a subset B ⊆ V of size r such that every vertex that is not in B, has an adjacent vertex in B. Prove that the vertex cover (VC) problem is polynomial time reducible to DSP. For simplicity, you may assume that VC remains NP-complete when restricted to input graphs with no isolated vertices (i.e., each vertex has at least one neighbor), and reduce from this version of VC if required.

   Useful terminology: Similar to the context of Vertex cover where an edge is covered by an endpoint vertex being included in the VC set, here, we say a vertex u is dominated if u itself or one of its neighbors is included in the dominating set (DS); thus, the DS solution is a set of vertices that collectively dominates all the vertices in the graph (similar to how a VC solution collectively covers all the edges).

   ###### Answer:

   To reduce Vertex Cover (VC) to Dominating Set (DS), transform the VC instance (G,k) into a DS instance (G′, k) as follows: 

   1. Construct G′ : For each edge e=(u,v) in G, add two new vertices w_e and x_e. Connect w_e to u, v, and x_e. This ensures x_e is a leaf only adjacent to w_e. 
   2. Reduction Argument: 
      - VC → DS: If S is a vertex cover in G, S is also a dominating set in G′. S covers all edges, so for every w_e, at least one of u or v is in S, dominating w_e and x_e. 
      - DS → VC: If B is a dominating set in G', replace any w_e ∈ B with one of its endpoints (u or v). This forms a vertex cover S in G of size ≤ |B|.

   The transformation is polynomial-time, and G has a VC of size k iff G' has a DS of size k. Thus, VC ≤ₚ DS.

3. Suppose you are a movie director. For your next movie, you are considering n actors that you like. You want the audience to witness all the new combinations of acting talent working together - i.e., you want to pick a set of actors from the n candidates, such that no two have worked together in a movie before. For this, you make a combined list of all the movies in which any of these actors have acted, giving you a total of m movies (thus, each of the movies features one or more of these n actors). You want to find at least k actors to cast for your movie such that no two have acted in the same movie before. Your input consists of n actors, m movies, along with the information of which actors have acted in which movies, and the number k. Prove that this problem of Novel Combination Casting (NCC) is.
   a) in NP.
   b) NP-hard (by choosing a suitable problem studied in class to show a poly-time reduction).

   ###### Answer:

   a) NP: Given a candidate cast of k actors, verify in O(k²m) time that no pair shares a movie.
   b) NP-hard: Reduce Independent Set to NCC:

   - Model actors as vertices.
   - For each movie, connect all its actors pairwise (forming a clique).
   - A size-k independent set in this graph = a valid NCC cast.
     Since Independent Set is NP-hard, NCC is too.

   Thus, NCC is NP-complete.

4. Given an undirected graph G = (V, E), and integer m, the CLIQUE problem is to decide if there is a subset A ⊆ V of vertices (called as a clique) of size at least m such that for every pair of vertices u, v ∈ A with $u \ne v$, (u, v) is an edge in E.
   The HALF-CLIQUE problem asks if G has a clique of size at least |V|/2 - Note that it does not take integer m as input unlike the CLIQUE problem. Show that HALF-CLIQUE is
   a) in NP.
   b) NP-hard by reducing from CLIQUE , which is known to be NP-complete.

   ###### Answer:
   a) NP: A certificate is a subset of ≥ |V|/2 vertices. Verify all pairs are edges in O(n²) time.
   
   b) NP-hard reduction from CLIQUE:
   
   - Case 1: If input CLIQUE size m ≥ |V|/2, output G directly. A clique of size m ≥ |V|/2 exists in G iff G has a half-clique.
   - Case 2: If m < |V|/2, build G′:
     - Add a clique S of size |V| − 2m, connecting all S vertices to every vertex in G. 
     - Total vertices in G′: |V| + (|V| − 2m) = 2(|V| − m). 
     - Half-clique size in G′: |V| − m.  
     - If G has a clique of size m, S U (clique in G) forms a clique of size |V| − m.  
     - If G′ has a half-clique, it must include ≥ m vertices from G, proving G has a clique of size ≥ m.

Thus, HALF-CLIQUE is NP-hard.
