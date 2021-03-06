# QuadSieve
by Thomas Panetti & Noemi Glaeser 
04/28/16
CSCE 557

About: 	This program is an implementation of the Multi-Precise Quadratic 
       	Sieve algorithm.

use:  	To compile this program, simply use the javac compiler
		javac QuadraticSieve.java
  	To run this file, run the class file with the input
		java QuadraticSieve [N] [Factorbase]
			EX: java QuadraticSieve 1037 100
        or simply run it and it will prompt you for input
		java QuadraticSieve

How:  	First, this program generates a list of primes (including -1) up 
	to the size of the factorbase using Eratosthenes sieve. For example,
	for a factorbase of 10 the primes list would be {-1, 2, 3, 5, 7}. Next, 
	the program populates an array from index -R to R, R being sqrt(N),
	with the values (R+n)^2 - N, n being the current index in -R to R.
	Next, we run a loop through every prime in the prime array and 
	attempt to divide each value in the array from -R to R by the
	prime. This is repeated with every prime in the factorbase. 

	Now we are left with an array of residuals after the division
	by every prime in the factorbase. Indices at which the residual
 	is equal to one represent numbers that are smooth over the 
	factorbase. We rebuild the prime factorization of the smooth numbers 
	using trial division, giving us a matrix with rows representing the
	individual smooth numbers (whose original indices are stored in a pair),
	and with columns representing the primes in the factorbase. Each entry
	stores the exponents of the prime factors of that particular smooth 
	number. We then reduce the matrix mod 2. 

	Lastly, we use Gauss-Jordan elimination to determine the combinations
	of rows (the rows represent values of n in the original array from -R
	to R) that sum to zero. For each combination, we rebuild the equation 
	(x^2 = y^2), where x^2 is the product of (R+n)^2 -N for each n in the 
	combination, and y^2 is the product of (R+n)^2 for each n in the 
	combination. Taking the gcd of N and x-y and of big N and x+y, we 
	(ideally) obtain two factors of N. By repeating this process with
	every combination obtained from Gauss-Jordan elimination, we try to get
	every possible factor of N. Finally, we do the division of every factor 
	by every other factor to make sure we have both factors of each composite 
	factor found.
