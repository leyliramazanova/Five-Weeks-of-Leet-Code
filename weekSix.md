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
