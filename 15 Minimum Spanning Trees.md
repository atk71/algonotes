### 15 Minimum Spanning Trees
### 15.1 Properties of Minimum Spanning Trees
Given a weighted undirected graph G, find a tree, T, that contains all the vertices of G, while minizing the sum total of all the edge weights. 

> Lemma 15.1: Let G be a weighted connected graph, and let T be a minimum spanning tree for T. If e is an edge of G that is not in T, then the weight of e is at least as great as any edge in the cycle created by adding e to T .

> Theorem 15.2: Let G be a weighted connected graph, and let V1 and V2 be a partition of the vertices of G into two disjoint nonempty sets. Furthermore, let e be an edge in G with minimum weight from among those with one endpoint in V1 and the other in V2. There is a minimum spanning tree T that has e as one of its edges.


### 15.2 Kruskal's Algorithm
> Algorithm 15.4: Kruskal’s algorithm for the MST problem.
> 
> Algorithm KruskalMST(G): 
> Input: A simple connected weighted graph G with n vertices and m edges 
> Output: A minimum spanning tree T for G
> for each vertex v in G do  
> 	Define an elementary cluster C(v) ← {v}.
> Let Q be a priority queue storing the edges in G, using edge weights as keys 
> T ← ∅ // T will ultimately contain the edges of the MST 
> while T has fewer than n − 1 edges do
> 	(u, v) ← Q.removeMin()
> 	Let C(v) be the cluster containing v
> 	Let C(u) be the cluster containing u
> 	if C(v) =/= C(u) then
> 		Add edge (v, u) to T
> 		Merge C(v) and C(u) into one cluster, that is, union C(v) and C(u)
> return tree T

> Lemma 15.3: Consider an execution of Kruskal’s algorithm on a graph with n vertices, where clusters are represented with sequences and with cluster references at each vertex. The total time spent merging clusters is O(n log n).

> Theorem 15.4: Given a simple connected weighted graph G with n vertices and m edges, Kruskal’s algorithm constructs a minimum spanning tree for G in O(m log n) time.

> Theorem 15.5: Given a simple connected weighted graph G with n vertices and m edges, with the edges ordered by their weights, we can implement Kruskal’s algorithm to construct a minimum spanning tree for G in O(m α(n)) time.