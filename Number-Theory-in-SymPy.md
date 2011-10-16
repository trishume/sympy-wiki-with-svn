### Elementary Number Theory in SymPy

##Prime factorization.
```python
>>> isprime(45)
False

>>> primefactors(45)
[3, 5]

>>> factorint(75)
{3: 1, 5: 2}

>>> [ prime(i) for i in range(1, 10)]  # prime(i) - returns the _i_th prime.
[2, 3, 5, 7, 11, 13, 17, 19, 23]

>>> P = primerange(50, 100)
>>> [p for p in P]
[53, 59, 61, 67, 71, 73, 79, 83, 89, 97]

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
```