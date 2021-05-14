# About
An efficient and approximation algorithm for counting frequency of values in a stream of data. It uses sublinear space, it may sometimes overcount a value.

# How does it work?

1. Select a bunch of hash functions (the more functions you have the more accurate the results).
2. Draw a Matrix, use hash functions as rows and maximum result of the hash function as columns.
3. Initialize the matrix with 0s.
4. For each stream value pass it through every hash function and increment the corresponding cell value in the matrix.
5. To find the count select the minimum cell value for the value


Let's say our stream looks like `A, B, A, D, A...`

And we have 4 hash functions and this is what they return for each alphabet:

| | h1 | h2 | h3 | h4 |
|---| -- | -- | -- | -- |
| A | 1 | 3 | 1 | 6 |
| B | 1 | 2 | 4 | 3 |
| D | 3 | 5 | 2 | 6 |

If we pass the alphabets of the stream through the hash functions the table will look like this:

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| - | - | - | - | - | - | - | - |
| h1 | 0 | 4 | 0 | 1 | 0 | 0 | 0 |
| h2 | 0 | 0 | 1 | 3 | 0 | 1 | 0 |
| h3 | 0 | 4 | 0 | 0 | 1 | 0 | 0 |
| h4 | 0 | 0 | 0 | 1 | 0 | 0 | 4 |

To find the count of `A` we will find the minimum of (h1, 1), (h2, 3), (h3, 1) and (h4, 6) i.e. Count `Min`imum of 4, 3, 4 and 4 therefore the answer is `3` which is correct as the stream had 3 As.