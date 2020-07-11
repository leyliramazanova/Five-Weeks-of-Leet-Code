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
    
    
- [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/submissions/)
  ```python
  class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        cur_sum = max_sum = nums[0]
        for i in range(1, len(nums)):
            cur_sum = max(nums[i], cur_sum + nums[i])
            max_sum = max(cur_sum, max_sum)
        return max_sum
   ```
   
   
- [Rotate Array](https://leetcode.com/problems/rotate-array/submissions/)
  ```python
  class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        
        n = len(nums)
        k = k % n
        
        start = count = 0
        
        while count < n:
            current_idx = start
            prev_num = nums[start]
            while True:
                next_idx = (current_idx + k) % n
                nums[next_idx], prev_num = prev_num, nums[next_idx]
                current_idx = next_idx
                count += 1
                
                if start == current_idx:
                    break
            start += 1
     ```

- [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
```python
  class Solution:
      def climbStairs(self, n: int) -> int:
          memo = [None] * n
          memo[0] = 0
          memo[1] = 2
          if n == 1 or n == 2:
              return memo[n - 1]

          for i in range(2, n):


              memo[i] = memo[i - 1] +2 + memo[i-2] 
          return memo[n-1]
 ```
 
 - [Move Zeros](https://leetcode.com/problems/move-zeroes/submissions/)
 ```python
 class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        count = 0
        for i in range(len(nums)):
            if nums[i] != 0:
                nums[count] = nums[i]
                count += 1
        while count < len(nums):
            nums[count] = 0
            count += 1
  ```
  
  
  - [Single Number](https://leetcode.com/problems/single-number/)

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        dicte = Counter(nums)
        for num in dicte:
            if dicte[num] == 1:
                return num
```

- [TwoSum](https://leetcode.com/problems/two-sum/submissions/)
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dicte = {}
        for idx, val in enumerate(nums):
            remain = target - val
            if remain in dicte:
                return [dicte[remain], idx]
            else:
                dicte[val] = idx
```

- [SubArray](https://leetcode.com/problems/maximum-subarray/)
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        cur = 0
        maxi = float('-inf')
        for num in nums:
            cur = cur + num
            maxi = max(cur, maxi)
            if cur < 0:
                cur = 0
        return maxi
```

- [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/submissions/)
  ```python
  class Solution:
      def maxProfit(self, prices: List[int]) -> int:
          start = None
          maxProfit = 0
          for stock in prices:
              if start is None:
                  start = stock
              else:            
                  if start >= stock:          
                      start = stock     
                  else:
                      profit = stock - start
                      maxProfit = max(profit, maxProfit)
          return maxProfit
  ```
  
- [Reverse a Linked List](https://leetcode.com/problems/reverse-linked-list/)
```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if not head:
            return None
        curNode = head
        prev = None
        while curNode.next:
            next_node = curNode.next
            curNode.next = prev
            prev = curNode
            curNode = next_node
            
        curNode.next = prev
        return curNode
```

- [Symmetric Tree](https://leetcode.com/problems/symmetric-tree/submissions/)
```python
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        return self.isSame(root, root)
    
    def isSame(self, root1, root2):
        if not root1 and not root2:
            return True
        if not root1 or not root2:
            return False
        cond1 = root1.val == root2.val
        cond2 = self.isSame(root1.left, root2.right) and self.isSame(root1.right, root2.left)
        return cond1 and cond2
```

- [Intersection of two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/submissions/)
```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        headA_set = set()
        while headA:
            headA_set.add(headA)
            headA = headA.next
        while headB:
            if headB in headA_set:
                return headB
            headB = headB.next
        return None
```

```python
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        lengthA = self.length(headA)
        lengthB = self.length(headB)
        diff = lengthA - lengthB
        if diff > 0:
            for i in range(diff):
                headA = headA.next
        elif diff < 0:
            for i in range(-diff):
                headB = headB.next
        if headA:
            prev1 = headA.val
        if headB:
            prev2 = headB.val
        while headA:
            if headA.val == headB.val and prev1 != 0 and prev2 != 0:
                return headA
            else:
                if headA:
                    prev1 = headA.val
                if headB:
                    prev2 = headB.val
                headA = headA.next
                headB = headB.next
        return None
```
