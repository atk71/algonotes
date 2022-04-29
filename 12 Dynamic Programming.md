### 12 Dynamic Programming
### 12.3 Telescope Scheduling
For a list, L, of observation requests, where each request *i* consists of:
- a requested start time, si, which is the moment when a requested observation should begin.
- a finish time, fi, which is the moment when the observation should finish (assuming it begins at its start time)
- a positive numerical benefit, bi, which is an indicator of the scientific gain to be had by performing this observation.

> Theorem 12.3: Given a list, L, of n observation requests, provided in two sorted orders, one by nondecreasing finish times and one by nondecreasing start times, we can solve the telescope scheduling problem for L in O(n) time.


### 12.4 Game Strategies
12.4.1 Coins in a Line
- M<sub>i,j</sub> = the maximum value of coins taken by Alice, for coins numbered i to j, assuming Bob plays optimally.
- Game decisions are made along the following rationale:
	- If j = i+1, then pick the larger of V\[i\] and V\[j\], and the game is over.
	- Otherwise, if coin i is chosen, then the total utility is:
		- min{M<sub>i+1,j-1</sub>, M<sub>i+2,j</sub>} + V\[i\]
	- Otherwise, if coin j is chosen, then the total utility is:
		- min{M<sub>i,j-2</sub>, M<sub>i+1,j-1</sub>} + V\[j\]
- We get the following recurrence equation:
	- With initial conditions, i = \[1, 2, ... , n-1\]
	- M<sub>i,j</sub> = max{min{M<sub>i+1,j-1</sub>, M<sub>i+2,j</sub>} + V\[i\], min{M<sub>i,j-2</sub>, M<sub>i+1,j-1</sub>} + V\[j\]}
	- M<sub>i,i+1</sub> = max{V\[i], V\[i+1]}


> Theorem 12.4: Given an even number, n, of coins in a line, all of known values, we can determine in O(n2) time the optimal strategy for the first player, Alice, to maximize her returns in the coins-in-a-line game, assuming Bob plays optimally.

### 12.5 Longest Common Subsequence

> Algorithm 12.10: Dynamic programming algorithm for the LCS problem.
> 
> Algorithm LCS(X, Y ):
> 	Input: Strings X and Y with n and m elements, respectively
> 	Output: For i = 0, . . . , n − 1, j = 0, . . . , m − 1, the length L\[i, j] of a longest common subsequence of X\[0..i] and Y \[0..j]
> 	for i ← −1 to n − 1 do 
> 		L\[i, −1] ← 0
> 	for j ← 0 to m − 1 do
> 		L\[−1, j] ← 0
> 	for i ← 0 to n − 1 do
> 		for j ← 0 to m − 1 do
> 			if X\[i] = Y\[j] then
> 				L\[i, j] ← L\[i − 1, j − 1] + 1
> 			else
> 				L\[i, j] ← max{L\[i − 1, j] , L\[i, j − 1]}
> 	return array L

> Theorem 12.5: Given a string X of n characters and a string Y of m characters, we can find the longest common subsequence of X and Y in O(nm) time.

### 12.6 0-1 Knapsack

> Algorithm 12.13: Dynamic programming algorithm for the 0-1 knapsack problem.
> 
> Algorithm 01Knapsack(S, W ):
> Input: Set S of n items, such that item i has positive benefit bi and positive integer weight wi; positive integer maximum total weight W
> Output: For w = 0,...,W, maximum benefit B[w] of a subset of S with total weight at most w
> for w ← 0 to W do
> 	B\[w] ← 0
> for k ← 1 to n do
> 	for w←W downto wk do
> 		if B\[w−wk] + bk > B\[w] then
> 			B\[w] ← B\[w − wk] + bk

> Theorem 12.6: Given an integer W and a set S of n items, each of which has a positive benefit and a positive integer weight, we can find the highest benefit subset of S with total weight at most W in O(nW ) time.
