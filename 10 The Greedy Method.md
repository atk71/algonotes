### 10 The Greedy Method
### 10.1 The Fractional Knapsack Problem

> Algorithm 10.3: A greedy algorithm for the fractional knapsack problem.
> 
> Algorithm FractionalKnapsack(S, W ): 
> Input: Set S of items, such that each item i ∈ S has a positive benefit bi and a positive weight wi; positive maximum total weight W
> Output: Amount xi of each item i ∈ S that maximizes the total benefit while not exceeding the maximum total weight W 
> for each item i ∈ S do 
> 	xi ← 0
> 	vi ← bi/wi // value index of item i 
> w ← 0 // total weight
> while w < W and S =/= ∅ do
> 	remove from S an item i with highest value index // greedy choice
> 	a ← min{wi, W − w} // more than W − w causes a weight overflow
> 	xi ← a
> 	w←w+a

> Theorem 10.1: Given a collection S of n items, such that each item i has a ben- efit bi and weight wi, we can construct a maximum-benefit subset of S, allowing for fractional amounts, that has a total weight W in O(n log n) time.


### 10.2 Task Scheduling

> Algorithm 10.6: A greedy algorithm for the task scheduling problem.
> 
> Algorithm TaskSchedule(T ):
> Input: A set T of tasks, such that each task has a start time si and a finish time fi
> Output: A nonconflicting schedule of the tasks in T using a minimum number of machines
> m ← 0 // optimal number of machines 
> while T =/= ∅ do
> 	remove from T the task i with smallest start time si
> 	if there is a machine j with no task conflicting with task i then
> 		schedule task i on machine j 
> 	else
> 		m ← m + 1 // add a new machine
> 		schedule task i on machine m

>Theorem 10.2: Given a set of n tasks specified by their start and finish times, the Algorithm TaskSchedule produces, in O(nlogn) time, a schedule for the tasks using a minimum number of machines.