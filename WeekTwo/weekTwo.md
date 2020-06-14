##W eek 2 - Data Structures

The focus of week 2 is on linked lists, strings and matrix-based questions. The goal is to learn the common routines dealing with linked lists, traversing matrices and sequence analysis (arrays/strings) techniques such as sliding window.

- [Reverse a Linked List](https://leetcode.com/problems/reverse-linked-list/)
    - Iterative Approach
    ```python
    class ListNode:
         def __init__(self, x):
             self.val = x
             self.next = None
    
      class Solution:
        def reverseList(self, head):
            prev = None
            while head:
                curr = head
                head = head.next
                curr.next =prev
                prev = curr
            return prev
    ```
  - Recursive Approach
  ```python
    class Solution:
        def reverseList(self, head):
            if not head or not head.next:
                return head
            
            curr_head = self.reverseList(head.next)
            head.next.next = head
            head.next = None
            
            return curr_head
    ```



- [Detect Cycle in a Linked List](https://leetcode.com/problems/linked-list-cycle/)
    - Expensive Hash Table Approach
    ```python
    class Solution:
        def hasCycle(self, head: ListNode) -> bool:
            setListNode = set()
            while head:
                if head in setListNode:
                    return True
                else:
                    setListNode.add(head)
                    head = head.next
            return False
    ```

    - Expensive Hash Table Approach
    
    ```python
    class Solution:
        def hasCycle(self, head: ListNode) -> bool:
            if not head or not head.next:
                return False
            p1 = head
            p2 = head.next
            while (p1 != p2) :
                if not p2 or not p2.next:
                    return False
                p1 = p1.next
                p2 = p2.next.next               
            return True
    ```
- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        max_area = 0
        left = 0
        right = len(height) - 1
        while left < right:
            max_area = max(max_area, min(height[left], height[right]) * (right - left))
            if height[left] > height[right]:
                right-=1
            else:
                left+= 1
        return max_area
```

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        max_area = 0
        area = 0
        left = 0
        right = len(height) - 1
        while left < right:
            l, r = height[left], height[right]
            if l < r:
                area = (right - left) * l
                while height[left] <= l and left < right:
                    left += 1
            else:
                area = (right - left) * r
                while height[right] <= r and right> left:
                    right -= 1
            if area > max_area:
                max_area = area
        return max_area
```
    Time Complexity: O(n), Space Complexity: O(1)
    
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/solution/)
   - Approach 1: List Traversal
```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        for i in range(len(nums) - 1):
            if nums[i + 1] < nums[i]:
                return nums[i+1]
        return nums[0]
```

    - Time Complexity: O(n), Space Complexity: O(1)
    
   - Approach 2: Binary Search
   
 ```python
        class Solution:
            def findMin(self, nums: List[int]) -> int:
                left, right = 0, len(nums) - 1
                while left < right:
                    mid = (left + right)//2
                    if nums[mid] > nums[right]:
                        left = mid + 1
                    else:
                        right = mid
                return nums[right]
```

    - Time Complexity: O(logn), Space Complexity: O(1)

- [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
```python
class Solution:
    def characterReplacement(self, s, k):
        
        # Dict keeping tracks of the frequency of the words in the window
        count = {}
        
        # max_count = count of the most frequently occuring element in the window
        # result = the size of the sub array that is returned
        # start = starting index of the window
        # end - ending index if the window
        max_count = result = start = 0
        
        for end in range(len(s)):
            count[s[end]] = count.get(s[end], 0) + 1
            max_count = max(max_count, count[s[end]])
            # (end - start + 1) = all possible replacements
            # max_count = non repalced
            # (end - start + 1) - max_count = replaced
            if (end - start + 1) - max_count > k:
                
            #Increase the window by 1 and remove the frequency of the starting window
                count[s[start]] -= 1
                start += 1
                
            result = max(result, end - start + 1)
            
        return result
                
            
        
          
```
- Longest Substring Without Repeating Characters
- Minimum Window Substring
- Number of Islands
- Remove Nth Node From End Of List
- Palindromic Substrings
- Pacific Atlantic Water Flow