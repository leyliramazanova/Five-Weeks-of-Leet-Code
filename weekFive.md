## 40 Easy Questions in a week to polish coding skills based on this [guide](https://learntocodetogether.com/top-150-leetcodes-best-practice-problems/)


- [Search Insert Position](https://leetcode.com/problems/search-insert-position/submissions/)
  - Binary Search
    ```python
    class Solution:
      def searchInsert(self, nums, target):
          beg, end = 0, len(nums)
          while beg < end:
              mid = (beg + end)//2
              if nums[mid] >= target and nums[mid -1] < target:
                  return mid
              elif nums[mid] >= target:
                  end = mid
              else:
                  beg = mid + 1
          return beg
      ```

- [House Robber](https://leetcode.com/problems/house-robber/)
  - Dynamic Programming - bottom up approach
    ```python
    class Solution:
      def rob(self, nums: List[int]) -> int:
          if not nums:
              return 0
          if len(nums) == 1:
              return nums[0]

          dp = [None] * len(nums)
          dp[0] = nums[0]
          dp[1] = max(nums[0], nums[1])
          for i in range(2, len(nums)):
              dp[i] = max(dp[i - 2] + nums[i], dp[i-1])
          return dp[len(nums) - 1]
      ```
      
  - Dynamic= recursive
  
  ```python
  class Solution:
    def rob(self, nums: List[int]) -> int:  
        n = len(nums)
        if not n:
            return 0
        memo = [None] * n
        
        def steal(n):
            if memo[n] != None:
                return memo[n]
            if n == 0:
                result = nums[0]
            elif n == 1:
                result = max(nums[0], nums[1])
            else:
                result = max(steal(n-1),  nums[n] + steal(n-2))
            memo[n] = result
            return result
        
        return steal(n -1)
    ```
