### 13 Graphs and Traversals

### 13.1 Graph Terminology and Representations
### 13.2 Depth-First Search
### 13.3 Breadth-First Search
> Algorithm 13.8: BFS traversal of a graph.
> 
> Algorithm BFS(G, s):  
> Input: A graph G and a vertex s of G.
> Output: A labeling of the edges in the connected component of s as discovery edges and cross edges.
> Create an empty list, L0  
> Mark s as explored and insert s into L0 
> i←0  
> while Li is not empty do
> 	create an empty list, Li+1
> 	for each vertex, v, in Li do
> 		for each edge, e = (v, w), incident on v in G do
> 			if edge e is unexplored then
> 				if vertex w is unexplored then
> 					Label e as a discovery edge  
> 					Mark w as explored and insert w into Li+1
> 				else
> 					Label e as a cross edge
> 	i←i+1

### 13.4 Directed Graphs
#### 13.4.1 Directed Graph Traversal

> Algorithm 13.11: A recursive description of the DirectedDFS algorithm for searching from a vertex, v.
> 
> Algorithm DirectedDFS(G, v):
> Label v as active // Every vertex is initially unexplored
> for each outgoing edge, e, that is incident to v in G do
> 	if e is unexplored then
> 		Let w be the destination vertex for e 
> 		if w is unexplored and not active then
> 			Label e as a discovery edge
> 			DirectedDFS(G, w)
> 		else if w is active then
> 			Label e as a back edge
> 		else
> 			Label e as a forward/cross edge
> Label v as explored

Three types of edges in a directed DFS Tree:
	1. back edges: connects a vertex to its parent
	2. forward edges: connects a vertex to its child
	3. cross edges: connects a vertex to a vertex that is neither parent nor child

> Theorem 13.16: Let Gì be a digraph. Depth-first search on Gì , starting at a vertex s, visits all the vertices of Gì that are reachable from s. Also, the DFS tree contains directed paths from s to every vertex reachable from s.

#### 13.4.4 Topological Ordering

>Algorithm 13.16: Topological sorting algorithm.
>Algorithm TopologicalSort(Gì ):  
>Input: A digraph Gì with n vertices.  
>Output: A topological ordering v1, . . . ,vn of Gì or Gì has a cycle.
>Let S be an initially empty stack 
>for each vertex u of Gì do
>	incounter(u) ← indeg(u) 
>	if incounter(u) = 0 then
>		S.push(u) 
>i←1
>while S is not empty do 
>	u ← S.pop()
>	number u as the i-th vertex vi
>	i←i+1
>	for each edge e ∈ Gì.outIncidentEdges(u) do
>		w ← Gì .opposite(u, e)
>		incounter(w) ← incounter(w) − 1
>		if incounter(w) = 0 then
>			S.push(w)
>if i > n then
>	return v1,··· ,vn
>return “digraph Gì has a directed cycle”

> Theorem 13.22: Let Gì be a digraph with n vertices and m edges. The topological sorting algorithm runs in O(n + m) time using O(n) auxiliary space, and either computes a topological ordering of Gì or fails to number some vertices, which indicates that Gì has a directed cycle.