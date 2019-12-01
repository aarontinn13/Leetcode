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
        
  
  **Time Complexity:** O(m*n) where m is the length of the first string and n is the length of the second string.
  **Space Complexity:** O(m*n) where m is the length of the first string and n is the length of the second string.
  
  
