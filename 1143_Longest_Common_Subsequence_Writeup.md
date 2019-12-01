# Solution

From the looks of it, this seems like a simple enough problem to solve in quadratic time and space using dynamic programming. We can simply create an M-by-N matrix (where M is the length of the first string and N is the length of the second string) and fill in the matrix with the count of the longest common subsequence as we iterate through each character of both strings. 

For each character in the first string, we can see if that character is the same as the character in the second string we are comparing to. If it is, we can fill in the matrix with the highest countincrement our count by 1, else we will continue to fill in the matrix with the highest length so far. The last element in the matrix is our answer.

Below is the solution written in python:

```python  
class Solution:
    def longestCommonSubsequence(self, string1: str, string2: str) -> int:
        ''' returns the longest common subsequence'''
        matrix = [[0]*(len(string2)+1) for i in range(len(string1)+1)]
        for i in range(len(string2)+1): #base cases
            matrix[0][i] = 0
        for i in range(len(string1)+1): #base cases
            matrix[i][0] = 0
        for i in range(1, len(string1)+1):
            for j in range(1, len(string2)+1):
                if string1[i-1] == string2[j-1]:
                    matrix[i][j] = (matrix[i-1][j-1]+1)
                else:
                    matrix[i][j] = max(matrix[i-1][j], matrix[i][j-1])
        return matrix[len(string1)][len(string2)]
```

**Time Complexity:** O(M\*N) 

**Space Complexity:** O(M\*N) 

*Where M is the length of the first string and N is the length of the second string.*

# Algorithm

1. Initialize an `M+1 by N+1` matrix where we will store the counts.
2. Set the first row of the matrix and first column of the matrix to zeroes as these are the base case.
3. Create an outer loop to iterate from `1` to `len(string1)+1` where the index `i` will be the index of the current letter of `string1`. 
4. Create an inner loop to iterate from `1` to `len(string2)+1` where the index `j` will be the index of the current lettter of `string2`.
5. If `string1[i-1]` is the same as `string2[j-1]`, we can increment the highest count seen by setting the current index of the matrix `matrix[i][j]` to `matrix[i-1][j-1]+1`.
6. Else, if `string1[i-1]` is not the same as `string2[j-1]`, we will set the current index of the matrix `matrix[i][j]` to the max value between `matrix[i-1][j], matrix[i][j-1]`
7. When the matrix is complete, return the last value in the matrix: `matrix[len(string1)][len(string2)]`

Below is an example of a finished matrix with the strings `ACD` and `ABCD` the solution: `3`

| 0 | 0 | 0 | 0 | 0 |
|---|---|---|---|---|
| **0** | 1 | 1 | 1 | 1 |
| **0** | 1 | 1 | 2 | 2 |
| **0** | 1 | 1 | 2 | 3 |
