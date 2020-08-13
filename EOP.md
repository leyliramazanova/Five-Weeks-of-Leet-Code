# EOP questions for 1 month

[Reverse Bits-4.3](https://leetcode.com/problems/reverse-bits/submissions/)
  ```python
  class Solution:
      def reverseBits(self, n):
          res, power = 0, 31
          while n:
              res += (n & 1) << power
              n = n >> 1
              power -= 1
          return res
  ```

Because binary numbers are represented through 2 being raised to power x and we are dealing with 32-bit unsigned integer, we start with power 31.
```n & 1``` is compares the right-most bit in n to 1 and if they are both 1 returns 1. This is done to see whether the leftmost bit of the final number is going to be 1 or 0.
``` << power ``` is the number of bits we want to shift the result of ```n & 1 ``` to the left.
```n >> 1``` reduces n by 1 bit from the right. E.g. 33 will be reduced to 16


[Rectangle Overlap-4.11](https://leetcode.com/problems/rectangle-overlap/submissions/)
  ```python
  class Solution:
      def isRectangleOverlap(self, rec1: List[int], rec2: List[int]) -> bool:
          if rec1 == rec2:
              return True
          x11, y11, x12, y12 = rec1[0], rec1[1], rec1[2], rec1[3]      
          x21, y21, x22, y22 = rec2[0], rec2[1], rec2[2], rec2[3]  

          bool_x1 = (x21 in range(x11+1,x12)) or (x22 in range(x11+1,x12))
          bool_x2 = (x11 in range(x21+1,x22)) or (x12 in range(x21+1,x22))

          bool_y1 = (y21 in range(y11+1,y12)) or (y22 in range(y11+1,y12))
          bool_y2 = (y11 in range(y21+1,y22)) or (y12 in range(y21+1,y22))

          return (bool_x1 or bool_x2) and (bool_y1 or bool_y2)
  ```

