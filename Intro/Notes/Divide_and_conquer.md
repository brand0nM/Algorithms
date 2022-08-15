# Divide and Conquer
	1) Divide into smaller subproblems
	2) Conquer via recursive calls
	3) Combine solutions into the original problem
### Motivation
#### The PROBLEM

	Input: array size n, containing every natural number <= n 
	(excluding zero), arranged in arbitray order
	Output: number of inversions; defined by integers i and j, 
	where i < j and array[i] > array[j]

	EX1:
		Input:		[1, 3, 5, 2, 4, 6]
		Output:
			Level 1:       (5, 2) 
			Level 2:   (3, 2)   (5, 4)

	Graphical: ordered vs unordered array by drawing corresponding 
	line segments; then the sum of intersections is the number of 
	inversions.

	Application: Numeric similarity is a measure between two ranked 
	list. In real life these list can be anything, from user 
	interaction to recent purchases; after finding other people 
	with similar preferences, the algorithm can recommend based on 
	other customers. This process is known as collaborative 
	filtering
		
	
#### Approach
	The maximum number of inversions (n 2) = n(n-1)/2

	Brute Force: O(n^2)

	Divide and Conquer:
		
		Recursive call on inversion i,j where i<j and the..
			... left inversion if i, j <= (n/2)
			... right inversion if i, j > (n/2)
			... split inversion if i <= (n/2) < j
		EX1, all inversions were split

### Abstract
	Count array length n
		if length =1 return 0
		else
			x = Count(left inversion, (n/2))
			y = Count(right inversion, (n/2))
			z = CountSplitInversion(array, (n/2))
		return x+y+z
	Goal: if CountSplitInversion can be linear, then the full 
	function can run O(nlogn). Recall how merge sort squashed linear
	terms. 

#### Handling Split Inversions
	Idea1: instead of counting then sorting our array, what if we 
	could sort while counting 
		if length =1 return 0
		else
			x = Sort&Count(left inversion, (n/2))
			y = Sort&Count((right inversion, (n/2))
			z = Merge&CountSplitInversion(array, (n/2))
		return x+y+z

#### Proof
	Claim: a split inversion involving an element y of the 2nd 
	array C are precisely the number left in the last array B when 
	y is copied to the output  D.

	Proof: Fix x as element in first array
		1) If x is copied first => x<y => no split inversions
		2) If y is copied first => y<x => x and y are split inversion

#### Merging and Counting Split Inversions

	Graph: [Array B]	[Array C]

			[Array D]


	While merging two split arrays, we will also keep a running total of the
	number of split inversions. When elements of the 2nd array C get copied 
	over to output D, increment the total by number of elements in 1st 
	array B 
