# Intermediate Level Problems


- [Rotate Image](https://leetcode.com/problems/rotate-image/submissions/)
  ```python
  class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        row = col = len(matrix)
        
        for i in range(row):
            for j in range(i, col):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
        
        for i in range(row):
            for j in range(col//2):
                matrix[i][j], matrix[i][-(j+1)] = matrix[i][-(j+1)], matrix[i][j]
        
        return matrix

  ```
