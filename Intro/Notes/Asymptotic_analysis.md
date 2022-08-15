# Asymptotic Analysis

### Motivation
An algorithms design can be visually represented by 'Big-Oh' graphs; Each one has a theoretical 'sweet-spot' for the algorithms that is independent of language, arcitecture and compiler. Its used to compare different algorithms operations/runtime and performace- especially as the input get large

#### High Level idea
Want to supress constant factors and lower-order terms; in this way we can reduce the output and ultimately save processsing power. Constant factors are determined by the system and are dependent on that environment, while lower-order terms are simply irrelevant for larger inputs

	Example: We equate 6nlog2n +6n with just nlogn

		Running time: O(nlogn)
	
	Example: Does an array contain the integer t

		for i=1 to n:
			if A[i] == t return TRUE
		return FALSE

		Running Time: is O(n) or Linear

	Example: Given 2 arrays of length n and target t

		for i=1 to n:
			 if A[i]==t return TRUE
		for i=1 to n:
			 if B[i]==t return TRUE
		return FALSE

		Running Time: O(n) since this is 2 Linear 
		searches mult by const 2; which get 
		suppressed in Big-Oh notation

	Example: Do n arrays A/B have a number in common?

		Nested Loops:
		for i=1 to n:
			for j=1 to n:
				if A[i]==B[j] return TRUE
		return FALSE
		
		Running Time: O(n^2) or Quadratic

	Example: Does an array have duplicate entries 
		
		for i=1 to n:
			for j= i+1 to n:
				if A[i]==A[j] return TRUE
		return FALSE

		Running Time: O(n^2) or Quadratic

	Essencially worry about the number of iterations
		
## Big-Oh Notation
let T(n) = function on n=1,2,... Big-Oh notation looks at the worst possible outcome for the function; OR when T(n)= O(f(n)). Eventually, for sufficently large n T(n) is bounded above by a constant multiple of f(n).

### Definition
T(n) = O(f(n)) if and only if there exist constants c, n_0>0 such that T(n)<=cf(n) for all n>=n_0

	where n_0 is the functions crossing points

	Example: prove if T(n)=a_kn^k+...+a_1n+a_0
	T(n)=O(n^k)

	Proof: choose n_0=1 and c=|a_k|+...+|a_1|
	For every n>=1, T(n) <= |a_k|n^k+...+|a_0| <=
	|a_k|n^k+...+|a_0|n^k = cn^k

	Example: for every k>=1, n^k is not O(n^k-1)

	Proof: Assume n^k=O(n^k-1) then ther exist 
	constants c, n_0>0 such that n^k <= cn^k-1 for 
	all n >= n_0, but then n<=c for all n>=n_o;
	Hence, contradiction

#### Big Omega
Defintion: T(n) = OMEGA(f(n)) iff there exist constants c,n_0 such that T(n) >= cf(n) for all n greater than or equal to n_0. n_0 is still the crossing point, but now cf(n_0) is the crossing point and our T(n) isbound above by the function f(n) and bellow by cf(n) where n>=n_0

#### Theta 
Defintion: T(n) = THETA(f(n)) iff T(n)=O(f(n)) and T(n) = OMEGA(f(n)) 

Equivalent: there exist constants c_1, c_2 n_0 such that c_1f(a) <= T(n) <= c_2f(n) for all n>=n_0; or the thetaa function is bound above and below by these two constants

#### Little-Oh
Definition: T(n) = o(f(n)) iff for all constants c>0 there exist a constant n_o such that T(n) <= cf(n) for all n >= n_0


	Example 1: 2^(n+10) = O(2^n)
	Proof: 2^(n+10)=2^n*2^10, let [c = 2^10, n_0=1]

	Example 2: 2^(10n) != O(2^n)
	By Contra: if true, there exists c and n_0, such that
	2^10n <= c2^n for all n>= n_0, but then divide by 2^n
	and 2^9n <= c for all n >= n_0

	Example 3: for every pair of positive functions 
	f(n), g(n); max{f, g} = THETA(f(n)+g(n))
	Proof: for every n, we have Max{f(n), g(n)} <= 
	f(n)+g(n) and f(n)+g(n) <= 2Max{f(n), g(n)}
	Thus 1/2(f(n)+g(n)) <= 2Max{f(n), g(n)} <= f(n)+g(n)

