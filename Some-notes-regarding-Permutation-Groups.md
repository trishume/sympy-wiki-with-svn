*# Permutation Groups #

## Preliminaries ##
A permutation can be represented as a function on a set of points and can also be represented in a cyclic notation. We normally do not write out cycles of length one (these are also called fixed points).
So if \[\pi = (0, 3 , 4, 1)(2)(5, 6)(7)\] then the fixed points are 2 and 7 and we rewrite it as
\[\pi = (0, 3 , 4, 1)(5, 6)\]

Multiplication of two permutations, say, \(\alpha\) and \(\beta\) are defined by function composition that is
(\(\alpha\)\(\beta\))(x) = \(\alpha\)(\(\beta\) x)

Thus we can see that composition of two permutations is again a permutation.

## Some basic algorithms ##

### Algorithm 1 ###
This is used to multiply permutations

#### MULT(n, \(\alpha\), \(\beta\), \(\gamma\)) ####

1. *for* i \(\Leftarrow\) 0 to n-1
    1. *do* \(\pi_{0}\)[i] \(\Leftarrow\) \(\alpha\)[\(\beta\)[i]]
2. *for* i \(\Leftarrow\) 0 to n-1
    1. *do* \(\gamma\)[i] \(\Leftarrow\) \(\pi_{0}\)[i]

Note that we use an auxiliary permutation here to prevent bugs arising because of modifications to the arrays \(\alpha\) & \(\beta\)

### Algorithm 2 ###
This is used to compute the inversion of a permutation

#### INV(n, \(\alpha\),) ####

1. *for* i \(\Leftarrow\) 0 to n-1
    1. *do* \(\beta\)[\(\alpha\)[i]] \(\Leftarrow\) i

### Algorithm 3 ###
This is used to convert a cycle to an array

CYCLE_TO_ARRAY (n, C)

1. *for* i \(\Leftarrow\) 0 to n-1
    1. *do* \(A\)[i]] \(\Leftarrow\) i

2. i \(\Leftarrow\) i
3. Set l to be the length of string C
4. *while* i < l: 
    1. if C[i] = "(" then:
        1. i \(\Leftarrow\) i + 1
        2. *if* C[i] \(\in\) {0, 1, ..., 9} then:
           1. Get x starting at i
           2. z \(\Leftarrow\) y
           3. Increment i to the position after x
    2. if C[i] = ","
        1. i \(\Leftarrow\) i + 1
        2. *if* C[i] \(\in\) {0, 1, ..., 9} then:
           1. Get y starting at i
           2. A[z] \(\leftarrow\) y 
           3. Increment i to the position after y
           4. x \(\Leftarrow\) y
    3. if C[i] = ")"
        1. A[x] \(\Leftarrow\) z
        2. i \(\Leftarrow\) i + 1

Similarly, we can construct an algorithm to convert an array to a cycle.

## Data structure to store a group ##

If we need to make use of a permutation group then we need to be able to
1. Efficiently store the group
2. Allow testing of membership to be done very rapidly
3. Enumerate all the elements of the group without repetition

Now, suppose we store a group as a list of lexicographically arranged permutations then we can observe a few things.

1. The space complexity in the worst case is n!
2. Testing membership using binary search is O(\(n^2\) \(\log(n)\))
3. Generating elements takes O(1) time

Alternatively, we can just store the generators. Enumeration of elements will then involve products in the generators of length one, length two and so on. We cross out duplicates as and when we need to.

### Algorithm 4 ###
Algorithm to generate a group \(\G\) from its generators \(\tau\)

#### SIMPLE_GEN (n, \(\tau\)) ####
1. \(G \) \(\Leftarrow\) \(\phi\)
2. New \(\Leftarrow\) {I}
3. while New != \(\phi\)
    1. \(G \) \(\Leftarrow\) \(G \) \(\cup\) New