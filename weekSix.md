## ??/40 Easy Questions in a week to polish coding skills based on this [guide](https://learntocodetogether.com/top-150-leetcodes-best-practice-problems/)


- [Merge Two Sorted Lists] (https://leetcode.com/problems/merge-two-sorted-lists/)
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
