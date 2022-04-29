### 14 Shortest Paths

### 14.1 Single-Source Shortest Paths
For a wieghted graph, G:
- the length or weight of a path, P, in G, is the sum of the weights of all edges of P
- for a source v, and a target u, both contained in G, the distance, denoted d(v, u), is the length of the shortest path from v to u, if such a path exists.

### 14.2 Dijkstra's Algorithm
A greedy method for finding shortest paths.

> Algorithm 14.2: Dijkstra’s algorithm for the single-source shortest path problem for a graph G, starting from a vertex v.
> 
> Algorithm DijkstraShortestPaths(G, v):
> 	Input: A simple undirected weighted graph G with nonnegative edge weights, and a distinguished vertex v of G
> 	Output: A label, D[u], for each vertex u of G, such that D[u] is the distance from v to u in G
> 	D[v] ← 0  
> 	for each vertex u à= v of G do
> 		D[u] ← +∞
> 	//Let a priority queue, Q, contain all the vertices of G using the D labels as keys. 
> 	while Q is not empty do
> 		// pull a new vertex u into the cloud
> 		u ← Q.removeMin()
> 		for each vertex z adjacent to u such that z is in Q do
> 			// perform the relaxation procedure on edge (u, z)
> 			if D[u] + w((u, z)) < D[z] then
> 				D[z] ← D[u] + w((u, z))
> 				Change the key for vertex z in Q to D[z]
> 	return the label D[u] of each vertex u

> Lemma 14.1: In Dijkstra’s algorithm, whenever a vertex u is pulled into the cloud, the label D[u] is equal to d(v, u), the length of a shortest path from v to u.

> Theorem 14.2: Given a simple weighted graph G with n vertices and m edges, such that the weight of each edge is nonnegative, and a vertex v of G, Dijkstra’s algorithm computes the distance from v to all other vertices of G in O(m log n) time, or, alternatively, in O(n2) time.