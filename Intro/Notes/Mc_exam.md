# Exam
## Question 1
	3-way-Merge Sort : Suppose that instead of dividing in half at each step of Merge Sort, you divide into thirds, sort each third, and finally combine all of them using a three-way merge subroutine. What is the overall asymptotic running time of this algorithm? (Hint: Note that the merge step can still be implemented in  time.)
	
	Logically:
		At each level j=[0,...,log_3(n)] there will be 3^j elements => 3^j=n iff j = log_3(n)
	Picture:
	Level 0:				[n element]
	Level 1:		[n/3 elements][n/3 elements][n/3 elements]
	.............................................................................
	Level log_3(n):  [single element][single element]......[single element][single element]
	
	Total Operations: for some constant C, 
			((C n) / (3^j)) 3^j = C n, per Level Operation
				and Cn(log_3(n) + 1) Total Operations, 
				O(Cn(log_3(n) + 1)) ≈ O(nlog_3(n))
					Answer D: O(nlog(n))

## Question 2:
	You are given functions f and g such that f(n) = O(g(n)). Is 
	f(n)*log_2(f(n)^c) = O(g(n)*log_2(g(n)))? (Here  is some positive constant.) 
	You should assume that f and g are nondecreasing and always bigger than 1.

	Proof: Since f(n) = O(g(n)), f(n) is bounded above by some constant C and function Cg(n), 
		or for all n, f(n) <= g(n),
			now take the product f(n)*log_2(f(n)^c) = f(n)*log_2(f(n))^c,
			log_2(f(n))^c term is at a maximum when c=1, so
			by the definition O(n), <= Cg(n)*log_2(Cg(n)) = Cg(n)*(log_2(C)+log_2(g(n)))
				O(Cg(n)*(log_2(C)+log_2(g(n)))) ≈ O(g(n)*log_2(g(n)))


## Question 3:
	Assume again two (positive) nondecreasing functions f and g such that f(n) =O(g(n)). i
	Is 2^f(n)=O(2^g(n))?
	
	Proof: by definition f(n) <= cg(n) for some constant c and n >=n_0.
		so 2^f(n) <= 2^cg(n) = K2^g(n) for some constant K. This 
		holds for a new fixed n_o´ <= n,so
			Answer A & B: yes if f(n)<=g(n)for all sufficently large n
			and Sometimes
		
## Question 4:
	k-way-Merge Sort. Suppose you are given k sorted arrays, each with n elements, and you want to combine them into a single array of kn elements. Consider the following approach. Using the merge subroutine taught in lecture, you merge the first 2 arrays, then merge the 3rd given array with this merged version of the first two arrays, then merge the 4th given array with the merged version of the first three arrays, and so on until you merge in the final (kth) input array. What is the running time taken by this successive merging algorithm, as a function of k and n? (Optional: can you think of a faster way to do the k-way merge procedure ?)

	1st merge runtime: 2n +
	2nd merge runtime: 3n +
	...................... +
	kth-1 merge runtime: (k-1)n	
	kth merge runtime: kn
	= (1+2+...+(k-1))n + (k-1)n = n(k(k-1)/2 + (k-1)) = n(k-1)(k/2-1)

		O(n(k-1)(k/2-1))≈O(nkk)=O(nk^2)

## Question 5:
	Arrange the following functions in increasing order of growth rate 
		(with g(n) following f(n) in your list iff f(n)=O(g(n))).

	(b)2^n < (c)2^(2^n) clearly

	Since logn < n, 2^logn < 2^n, and clearly 2^log(n) < n^log(n)
		WTS. n^log(n) < 2^n

		for n=0,1,..., 
			and as n => infinity, l'hops => n^log(n)ln(n)/n < ln(2)2^n
					l'hops => n^log(n)ln(n)^2/n^2 < ln(2)^2 2^n
					...
	(d)n^log(n) < (b)2^n
		
	n^2 < Kn^2 when K is greater than 1, take K = log(n), 
		then when n>10,n^2 < log(n)n^2
		l'hops => 2n < n + 2nlog(n)
	(e)n^2 < (a)log(n)n^2

	finally, 
		log(n)n^2 < n^log(n)?
		l'hops => n + 2nlog(n) < n^log(n)ln(n)/n 
		l'hops => 1 + 2 + 2log(n) < n^log(n)ln(n)^2/n^2 
		l'hops => 2/n < n^log(n)ln(n)^3/n^3

	Hence (e)<(a)<(d)<(b)<(c) 
