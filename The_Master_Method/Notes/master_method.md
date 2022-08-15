# The Master Method

## Review/Direction
	Motivation: Potentially useful algorithmic ideas often need mathematical analysis

	Recall: Grade school algorith has a O(n^2) runtime

	Approach: split numbers into left and right half a,b and c,d respectively, 
	then the product of 
	X*Y = 10^nac+10^(n/2)(ad+bc) + bd
	Then T(n) is the maximum number of operations this algorithm needs to 
	multiply two n-digit numbers
	


	Recurrence: express T(n) in terms of the running times of each recursive call

		Basecase: if T(1) <= by a constant
		For all n>1: T(n) <= 4T(n/2) + O(n)
			inside: at each level 4 calls on n/2 elements
			outside: After add terms up which runs linear



	Gauss's Recursive Algorithm: compute quantities ac, bd, and (a+b)(c+d), 
	then (ad+bc) = (a+b)(c+d)-ac-bd
		Basecase: if T(1) <= by a constant
		For all n>1: T(n) <= 3T(n/2) + O(n)
			inside: at each level 3 calls on n/2 elements
			outside: After add terms up which runs linear

	Runtime: not obvious, will use master method
	in later lecture to uncover mechanism

## Formal Statement

	Blackbox for recurrences
		input: recurrence in particular format
		output: solution/upperbound to recurssion
	Assumptions: all subproblem have equal size.
		Basecase: if T(n) <= by a constant
			for sufficiently small n.
		For all larger n: T(n) <= aT(n/b)+O(n^d)
		a, # recursive calls (>=1)
		b, factor by which input shrinks (>1)
		d, Exponent of runtime of the combine step (>=0)
	An algorithm that makes a recursive calls on subproblems of equal size 
	T(n/b), with n^d work done outside, in the combine step
	
	Def: 3 cases
		    | O(n^dlog(n))     if a=b^d
	     T(n) = | O(n^d)           if a<b^d
		    | O(n^log_b(a))     if a>b^d

		Reason 1st case doesnt have log_b is because log_b ≈ log, 
		differ by a constant
### Examples

	EX1: MergeSort, a=2, b=2, d=1 => Case1, so T(n) <= O(nlogn)
	EX2: BinarySearch, a=1, b=2, d=0 => Case1, so T(n) <= O(logn)
	EX3: 1st recursive int mult, a=4, b=2, d=1, Case3, so T(n) <= O(n^2)
	EX4: Gauss's recursive int, a=3, b=2, d=1, Case3, so T(n) <= O(n^log_2(3))
	EX5: Strassen, a=7, b=2, d=linear in matrix size or n, in this case 2
			Case3, T(n) <= O(n^log_2(7)) = O(n^2.81)
	EX6: Same as merge but combine is n^2, so a=b=c=2
			Case2: T(n) <= O(n^2)

### Proof
	
	Assume: recurrence is
		i) T(1) <= c for some constant c
		ii) T(n) <= aY(n/b) + cn^d
	and n is a power of b (general case is similar, but more tedious)
	

	Idea: Generalize MergeSort analysis, using a recursion tree
	At each level j=0,...log_b(n) There are a^j and n/b^j


	Graphically:

	Level0:                  [input size n]
	level1: [n/b][n/b][n/b][n/b]........[n/b][n/b][n/b][n/b],  a times
	..................................................................
	level log_b(n): [single el][single el].....[single el][single el], n times


	Single Level: Total work at single level j, 
		ignoring work in recursive calls <= 
			a^j (num subproblems)x c(n/(b^j))^d (size of each subproblem)
		= cn^d(a/b^d)^j
	All Levels: Totalwork <= cn^d(SUM[from j=o to log_b(n)](a/b^d)^j))


	Interpretaion of 3 cases: 
		Opposing forces
			a: rate of subproblems proliferation growing per level (RSP)
			b^d: rate of work shrinkage per level (RWS)
		Case1: There is a tie between the inversly proportional growths
		Case2: The RWS is greater than the RSP => bott grows faster
		Case3: The RSP is greater than the RWS => the num grows faster
	Intuition of 3 cases:
		1) RSP=RWS => same amount of work at each level
			Like MergeSort => expect O(n^dlog(n)) 
		2) RSP<RWS => less work each level => most work at root level
			Can assume work at other levels is negligable, so 
			amount of total work is equivalent to amount of root work
			or O(n^d)
		3) RWS<RSP => More work at each level => most work at the Leaves 
			so can assume they govern algorithm runtime, expect 
			O(#leaves)
	Proof:
		Total Work <= cn^d(SUM[j=0 to log_b(n)](a/b^d)^j)
			Case1: if a=b^d, then <= O(n^dlog(n)) 

			Case2: if a<b^d, then cn^d(SUM[j=0 to log_b(n)](a/b^d)^j)
				<= O(n^d)
			total amount only constant factor greater than top level
				Since a/b^d < 1

			Case3: if a>b^d, then Total Work <= constant largest term
			Total Work = cn^d((a/b^d)^log_b(n) - 1)/(a/b^d -1)
			total amount only constant factor greatest at leave level
				since a/b^d > 1, choose largest sum times n^d
				<= O(n^d(a/b^d)^log_b(n))

				aside: b^-dlog_b(n) = n^-d
				= O(a^log_b(n))

	The number of leaves in recursion tree is equal to a^log_b(n)







