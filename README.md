# benchmarking-dasg
## TODO:
Fix the deque update for upper bound to handle case where edge is not included. should be constant lookup time (adjacency matrix) ( _pbar +=2 )

## Summary
Jim_Elim:
This algorithm iterates through a stack of weighted edges. The weights correspond to upper bounds for the cost of mapping between the vertices in the graph.
There are 2 primary cases we consider as we cycle through the stack:  
Case A: The upper bound of ij is over our budget:
In this case, we will compute the true value of  matching score of edge ij, leading to subcases A1 or A2.
A1. If it is underbudget then we will tighten the bound, and left-append to the stack, resulting in the next iteration leading to case B.  
A2. Otherwise, if the true value of the matching score of edge ij is overbudget, then we will
	   1. eliminate this edge
	   2. increment the upperbounds of the adjacent edges by two.
	

Case B: the upper bound ij is not over our budget. We will then order the elements of the stack by their upperbounds. Using a heap, which takes O( n log n) time. each element is popped and then inserted into the heap, and then
popped from the heap and left appended to the stack. This means the edge with the greatest upper bound is at the top. We can then check upon each iteration if the top of the stack is overbudget. If not, then we can terminate.


#
idea: we could use the dummy/v ratio as a lazy evaluation of buildcostmatrix
rather than computing it each time, and we could maintain 'bins' based on the ratio. roundrobin evaluation of ratios. This would be justified since after the top of the stack is processed, if an elimination occurs, the next item on the stack is not necessarily the highest priority. 