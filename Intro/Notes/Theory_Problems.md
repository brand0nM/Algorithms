# Theory Problems
	1) You are given as input an unsorted array of n distinct numbers, where n is a power of 2. 
	Give an algorithm that identifies the second-largest number in the array, and that uses at most n+log_2(n)-2 comparisons.

		Input: unsorted array with n elements, n is evenly divisible by 2

		Essentially merge sort algorithm, except instead of sorting last split, return the minimal element

		def Comparision(array, starting_length):
			if length(array) != 1:
				middle = length(array)/2
				left = array[middle:]	
				right = array[:middle]

				Comparision (left)
				Comparision (right)
				
				i=j=k=0

		

	2) You are a given a unimodal array of n distinct elements, meaning that its entries are in increasing order up until its 
	maximum element, after which its elements are in decreasing order. Give an algorithm to compute the maximum element that 
	runs in O(log n) time.



	3) You are given a sorted (from smallest to largest) array A of n distinct integers which can be positive, negative, or zero. 
	You want to decide whether or not there is an index i such that A[i] = i. Design the fastest algorithm that you can for solving 
	this problem.
