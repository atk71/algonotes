### 18 Approximation Algorithms
Calculating approximate ratios to NP-complete problems save time, money, and resources. Using polynomial-time algorithms to approximate such NP-hard problems is one of the most effective methods.

### 18.1 The Metric Traveling Salesperson Problem
A metric version of TSP is constructed such that the edge weights satisfy the *triangle inequality*. 
	- For any three edges (u, v), (v, w), and (u, w) in G:
	- where c(e) represents the integer weight for an edge *e*
	- c((u, v)) + c((v, w)) $\ge$ c((u, w))

>THM 18.1: There is a 2-approximation algorithm for the Metric-TSP optimization problem that runs in polynomial time.

### 18.2 Approximations for Covering Problems
#### 18.2.1 A 2-Approximation for VERTEX-COVER

> Algorithm 18.6: A 2-approximation algorithm for VERTEX-COVER.
> 
> Algorithm VertexCoverApprox(G):
> 	Input: A graph G
> 	Output: A small vertex cover C for G
> 	C←∅
> 	while G still has edges do
> 		select an edge e = (v,w) of G
> 		add vertices v and w to C
> 		for each edge f incident to v or w do
> 			remove f from G 
> 	return C

> Theorem 18.3: There is a 2-approximation algorithm for the VERTEX-COVER problem that runs in O(n + m) time on a graph with n vertices and m edges.