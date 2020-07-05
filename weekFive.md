## 40 Easy Questions in a week to polish coding skills based on this (guide)[https://learntocodetogether.com/top-150-leetcodes-best-practice-problems/]


- [Search Insert Position] (https://leetcode.com/problems/search-insert-position/submissions/)
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
