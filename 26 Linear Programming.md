### 26 Linear Programming
Optimization problems:
- satisfying a set of constraints.
- an objective function to maximize or minimize the value for each constraint.

Steps to convert an optimization problem to an LP:
1. determine the variables or constraints.
2. find the quantities to optimize, with respect to the variables.
3. write equations that reflect the inequalities that express said constraints.

### 26.1: Formulating the Problem
Standard Form:
- for a linear function f:
	- f(x<sub>1</sub>, x<sub>2</sub>, ... , x<sub>n</sub>) = a<sub>1</sub>x<sub>1</sub> + a<sub>2</sub>x<sub>2</sub> + ... + a<sub>n</sub>x<sub>n</sub> = sum of {i = 0..n}: a<sub>i</sub>x<sub>i</sub>
- converted to standard form for an optimization problem:
	- maximize: z = the sum of all c<sub>i</sub>x<sub>i</sub>, i $\in$ V
	- Subject to: 
		- the objective function: 
			- the sum of all a<sub>ij</sub>x<sub>j</sub> ≤ b<sub>i</sub> for i $\in$ C, j $\in$ V
		- the nonnegative constraints:
			- x<sub>i</sub> $\ge$ 0 for i $\in$ V 

Convexity:
	- Feasible region: 
		- a set of all feasible points or solutions.
		- the geometric shape of a polygon.
	- A region is *convex* if any two arbitrary points in the region can be connected by a line segment contained by the polygon. 

### 26.4 Applications of Linear Programming
Shortest Paths:
- Given a source, *s*, and target, *t*, and a graph with each edge (u, v) having a weight, d(u, v), that represents the distance b/w u and v.
- To solve using LP:
	- max: d<sub>t</sub>
	- subject to the constraints: 
		- d<sub>s</sub> = 0
		- d<sub>v</sub> $\le$ d<sub>u</sub> + d(u, v), for every edge, (u, v)
- based on the Bellman-Ford algo (14.3)
	- uses the triangle inequality.