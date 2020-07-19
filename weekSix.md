## ??/40 Easy Questions in a week to polish coding skills based on this [guide](https://learntocodetogether.com/top-150-leetcodes-best-practice-problems/)


- [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
  ```python
  class Solution:
      def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
          merged = ListNode(0)
          copy = merged
          while l1 or l2:
              if not l1:
                  merged.next = l2
                  return copy.next
              if not l2:
                  merged.next = l1
                  return copy.next
              l1_val = l1.val
              l2_val = l2.val
              if l1_val < l2_val:
                  merged.next = ListNode(l1_val)
                  l1 = l1.next
                  merged = merged.next 
              else:
                  merged.next = ListNode(l2_val)
                  l2 = l2.next
                  merged = merged.next 

          return copy.next
  ``` 

- [Path Sum III](https://leetcode.com/problems/path-sum-iii/submissions/)
  ```python
  class Solution:
      def pathSum(self, root: TreeNode, sum: int) -> int:
          if not root:
              return 0
          self.count = 0
          self.dfs({}, 0, root, sum)
          return self.count

      def dfs(self, store, pathSum, node, sum):
          pathSum += node.val
          if pathSum == sum:
              self.count += 1
          diff = pathSum - sum
          self.count += store.get(diff, 0)
          store[pathSum] = store.get(pathSum, 0) + 1

          if node.left:
              self.dfs(store, pathSum, node.left, sum)
          if node.right:
              self.dfs(store, pathSum, node.right, sum)
          store[pathSum] -= 1
  ```
    
    
- [Reverse Integer](https://leetcode.com/problems/reverse-integer/)
  ```python
  class Solution:
      def reverse(self, x: int) -> int:    
          boole = False
          if x < 0:
              x = x * -1
              boole = True
          rev = 0
          while x > 0:
              pop = x % 10
              rev = rev * 10 + pop
              x = x // 10

          rev = -1 * rev if boole else rev
          if rev < (-2) ** 31 or rev >= (2**31 -1):
              rev = 0
          return rev
  ```
  
- [Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/submissions/)
  ```python
    class Solution:
      def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
          if not t1:
              return t2
          if not t2:
              return t1
          t1.val += t2.val
          t1.left =  self.mergeTrees(t1.left, t2.left)
          t1.right =  self.mergeTrees(t1.right, t2.right)
          return t1
  ```


- [Invert Binary Tree](https://leetcode.com/problems/merge-two-binary-trees/submissions/)
  ```
  class Solution:
      def invertTree(self, root: TreeNode) -> TreeNode:
          if not root:
              return None
          root.left, root.right = root.right, root.left
          self.invertTree(root.left)
          self.invertTree(root.right)
          return root
  ```

- [Majority element](https://leetcode.com/problems/majority-element/solution/)
```
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        keyMap = {}
        n = len(nums)
        for num in nums:
            keyMap[num] = keyMap.get(num, 0) + 1
            if keyMap[num] > n // 2:
                return num
        return None
```

- [Find All Numbers Disappeared in An Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/submissions/)
```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        length = len(nums)
        for i in range(length):
            val = abs(nums[i]) - 1
            nums[val] = abs(nums[val]) * - 1
        result = []
        for i in range(length):
            if nums[i] > 0:
                result.append(i + 1)
        return result
```

- [Is Palindrome Number](https://leetcode.com/problems/palindrome-number/submissions/)
  ```python
  class Solution:
      def isPalindrome(self, x: int) -> bool:
          copy_x = x
          if x < 0:
              return False
          revert = 0
          while x > 0:
              revert = revert*10 + (x%10)
              x = x // 10
          return (copy_x == revert)
  ```
  
 - [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/submissions/)
```python
class Solution:
  def longestCommonPrefix(self, strs: List[str]) -> str:
      if not strs:
          return "" 
      if len(strs) == 1:
          return strs[0]
      result = ""
      f_str = strs[0]
      for i in range(len(f_str)):
          cur_char = f_str[i]
          for j in range(1, len(strs)):
              if i > len(strs[j]) - 1:
                  return result
              comp_char = strs[j][i]
              if comp_char != cur_char:
                  return result
          result += cur_char
      return result
  ```

- [Shortest Unsorted Array](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/)
```
class Solution:
    def findUnsortedSubarray(self, nums: List[int]) -> int:
        start = stop = None
        n = len(nums)
        for i in range(n):
            smallest, idx = nums[i], i
            for j in range(i, n):
                if nums[j] < smallest:
                    smallest, idx = nums[j], j
            if idx != i:
                if not start and not stop:   
                    start = i
                    stop = idx  
                stop = max(stop, idx)   
            nums[idx], nums[i] = nums[i], nums[idx]
        if start or stop:
            return stop - start + 1
        else:
            return 0
```

```python
class Solution:
    def findUnsortedSubarray(self, nums: List[int]) -> int:
        sortedNums = sorted(nums)
        start = len(nums)
        end = 0
        for i in range(len(nums)):
            if nums[i] != sortedNums[i]:
                start = min(start, i)
                end = max(end, i)
                
        count = (end - start) + 1
           
        return count if count >= 0 else 0
``` 

- [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/submissions/)
```python
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        fast = head
        slow = self.reverse(slow)
        
        while slow:
            if fast.val != slow.val:
                return False
            fast = fast.next
            slow = slow.next
        return True
    
    def reverse(self, head):
        if not head:
            return
        prev = None
        while head:
            next = head.next
            head.next = prev
            prev = head
            if next:
                head = next
            else:
                break
        return head
```

- [Island Perimeter](https://leetcode.com/problems/island-perimeter/submissions/)

```python
class Solution:
    def islandPerimeter(self, grid: List[List[int]]) -> int:
        def dfs(grid, row, col, perimeter, visited):
            stack = collections.deque()
            stack.append((row, col))
            visited.add((row, col))
            len_col = len(grid[0])
            len_row = len(grid)
            while stack:
                o_row, o_col = stack.popleft()
                movements = [(0,1), (0,-1), (1,0), (-1,0)]
                for r, c in movements:
                    ro = o_row + r
                    co = o_col + c
                    if (ro in range(len_row)) and (co in range(len_col)) and grid[ro][co] == 1:
                        if (ro, co) not in visited:
                            visited.add((ro, co))
                            stack.append((ro, co))
                    else:
                        perimeter += 1
            return perimeter
                
        for row in range(len(grid)):
            for col in range(len(grid[0])):
                el = grid[row][col]
                if el == 1:
                    return dfs(grid, row, col, 0, set())
```  
