### Elementary Number Theory in SymPy

##Prime factorization.
```python
>>> isprime(45)
False

>>> primefactors(45)
[3, 5]

>>> factorint(75)
{3: 1, 5: 2}

>>> divisors(150)
[1, 2, 3, 5, 6, 10, 15, 25, 30, 50, 75, 150]
>>> divisor_count(150)
12

>>> [ prime(i) for i in range(1, 10)]  # prime(i) - returns the _i_th prime.
[2, 3, 5, 7, 11, 13, 17, 19, 23]

>>> P = primerange(50, 100)
>>> [p for p in P]
[53, 59, 61, 67, 71, 73, 79, 83, 89, 97]

# To find the greatest integer m such that p**m divides n.
>>> [multiplicity(5, n) for n in [8, 5, 25, 125, 250]]
[0, 1, 2, 3, 3]

>>> primorial(10)  # Product of first 10 prime numbers
6469693230

# To prove that there are infinitely many primes
>>> factorint(primorial(10) + 1)
{331: 1, 571: 1, 34231: 1}
# None of [331, 571, 34231] are among the first 10 primes.

# Next prime after 10
>>> nextprime(10)
11
# 4th prime after 10
>>> nextprime(10, 4)
19
>>> prevprime(10)
7
>>> [randprime(10, 100) for i in range(5)] # random prime in the given range
[79, 67, 41, 37, 23]


# No of primes below N
>>> primepi(100)
25
# Prime Number Theorem
>>> pp = primepi(10**8)
>>> a = (10**8) / ln(10**8)
>>> pp / a
1.06129923175648
```

## GCD and LCM
```python
>>> gcd(4369, 42823)
17
>>> lcm(436, 428)
46652

# Bezout's identity
>>> x, y, d = gcdex(4545, 4505)
>>> x, y , d
(338, -341, 5)
>>> d == 4545 * x + 4505 * y
True
```

## Partition function
```python
>>> npartitions(10)
42
```

## Euler's Totient function
```python
>>> totient(100)
40
>>> F = factorint(100)
>>> [totient(pow(p, e)) for p, e in F.iteritems()]
[2, 20]
# Hence, totient(100) = totient(2**2) * totient(5**2)
>>> n = 1435234
>>> sum([totient(d) for d in divisors(n)]) == n
True
```


## Residue Theory
```python
>>> is_primitive_root(3, 7)
True
>>> [i for i in divisors(7 - 1) if (3**i) % 7 == 1]
[6]
>>> n_order(3, 7)
6

>>> is_primitive_root(4, 7)
False
>>> [i for i in divisors(7 - 1) if (4**i) % 7 == 1]
[3, 6]
>>> n_order(4, 7)
3

# Legendre and Jacobi symbols and quadratic residue
>>> [j for j in range(7) if is_quad_residue(j, 7)]
[0, 1, 2, 4]
>>> list(set([i**2 % 7 for i in range(7)]))
[0, 1, 2, 4]
>>> [legendre_symbol(i, 7) for i in range(7)]
[0, 1, 1, -1, 1, -1, -1]

>>>  R = [i for i in range(45) if jacobi_symbol(i, 45) == -1]; R
[2, 7, 8, 13, 17, 22, 23, 28, 32, 37, 38, 43]
>>> [i for i in range(45) if (i**2) % 45 in R]
[] 

# Relation between Lagendre and Jacobi symbol.
>>> L = legendre_symbol
>>> factorint(45)
{3: 2, 5: 1}
>>> jacobi_symbol(7, 45) == L(7, 3)**2 * L(7, 5)**1
True
```

```python
# perfect_power(n) returns integers (b, e) s.t. n == b**e if exist.
>>> perfect_power(1000)
(10, 3)
>>> perfect_power(1001)
False
```

