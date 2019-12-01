From the looks of it, this seems like a simple enough problem to solve in quadratic time and space using dynamic programming. We can simply create an M-by-N matrix (where M is the length of the first string and N is the length of the second string) and fill in the matrix with the count of the longest common subsequence as we iterate through each character of both strings. 

For each character in the first string, we can see if that character is the same as the character in the second string we are comparing to. If it is, we can fill in the matrix with the highest countincrement our count by 1, else we will continue to fill in the matrix with the highest length so far. The last element in the matrix is our answer.

Below is the solution written in python.

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

**Time Complexity:** O(m\*n) where m is the length of the first string and n is the length of the second string.
  
**Space Complexity:** O(m\*n) where m is the length of the first string and n is the length of the second string.


| 0 | 0 | A | B | C | D |
|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 |
| A | 0 | 1 | 1 | 1 | 1 |
| C | 0 | 1 | 1 | 2 | 2 |
| D | 0 | 1 | 1 | 2 | 3 |
