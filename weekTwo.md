## Week 2 - Data Structures

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
- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
    - Sliding Window Inefficient Approach
    ```python
        class Solution:
            def lengthOfLongestSubstring(self, s: str) -> int:
                if len(s) == 1:
                    return 1
                start = result = max_count = 0
                non_repeating = {}
                for end in range(len(s)):
                    current = s[end]
                    if current not in non_repeating.values():
                        non_repeating[end] = current
                    else:
                        keys = list(non_repeating.keys()).copy()
                        end_one = end
                        for i in keys:
                            if non_repeating[i] == s[end]:
                                end_one = i
                                del non_repeating[i]
                                break
                            if i <= end_one:
                                del non_repeating[i]
                        non_repeating[end] = current
                    
                    max_count = len(non_repeating)
                    result = max(max_count, result)
                return result
    ```
  - Sliding Window Optimised
  
  ```python
    class Solution:
        def lengthOfLongestSubstring(self, s: str) -> int:
            start = 0
            max_len = 0
            used_set = {}
            for end in range(len(s)):
                if s[end] in used_set and start <= used_set[s[end]]:
                    start = used_set[s[end]] + 1
                else:
                    max_len = max(max_len, end - start + 1)
                used_set[s[end]] = end
            return max_len
    ```
  
- [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/solution/)

```python
class Solution:
    def minWindow(self, s, t):
        
        #minor optimisation
        if s == t:
            return s

        # The sliding window with a count of all unique characters
        window = {}
        
        #What the ideal counter would look like
        ideal = Counter(t)
        start = end = 0
        range1 = range2 = None
        max_len, progress,  required = float("inf"), 0, len(ideal)
        
        for end in range(len(s)):
            
            #consider each element
            elem = s[end]
            window[elem] = window.get(elem, 0) + 1
            
            # elem under condideration has same number of counts in ideal and windoq
            if elem in ideal and window[elem] == ideal[elem]:
                progress += 1
                
            
            #decreasing the size of the window
            while start <= end and progress == required:
                
                if end - start + 1 < max_len:
                    max_len = end - start + 1
                    range1, range2 = start, end
                    
                if ideal == window:
                    return s[range1 : range2 + 1  ]
                
                elem_curr = s[start]
                window[elem_curr] -= 1
                
                if elem_curr in ideal and window[elem_curr] < ideal[elem_curr]:
                    progress -= 1       
                start += 1  
            end +=1
            
        return "" if max_len == float("inf") else s[range1 : range2 + 1]
```

    Time Complexity:  O(∣S∣+∣T∣) where |S| and |T| represent the lengths of strings  S and T.

- [Number of Islands](https://leetcode.com/problems/number-of-islands/submissions/)
```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        
        if not grid:
            return 0
        
        row = len(grid)
        column = len(grid[0])
        no_of_islands = 0
        
        visited = set()
        
        def bfs(ro, col):
            stack = collections.deque()
            stack.append((ro, col))
            
            while stack:
                #.pop- is a dfs solution
                # .popleft - is a bfs solution
                row_pop, col_pop = stack.pop()
                #top, bottom, left, right
                directions = [[1, 0], [-1,0], [0,1], [0,-1]]
                for r1, c1 in directions:
                    r = r1 + row_pop
                    c = c1 + col_pop
                    if (r in range(row)) and (c in range(column)) and grid[r][c] == "1" and (r,c) not in visited:
                        visited.add((r, c))
                        stack.append((r,c))
        
        for ro in range(row):
            for col in range(column):
                element = grid[ro][col]
                
                if element == "1" and (ro, col) not in visited:
                    bfs(ro, col)
                    no_of_islands += 1
        return no_of_islands
```

    Time Complexity:  O(N) where N represents the length of the 2d array
    
- [Remove Nth Node From End Of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/submissions/)

```python
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        
        dummy = ListNode(0)
        dummy.next = head
        
        
        point_1 = dummy
        point_2 = dummy
        
        for i in range(n + 1):
            point_2 = point_2.next
        
        while point_2 != None:
            point_2 = point_2.next
            point_1 = point_1.next
        point_1.next = point_1.next.next    
        return dummy.next
```
- [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/submissions/)
```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        
        def expandFromMiddle(s, left, right):
            counter = 0
            while (left >= 0 and right < len(s) and s[left] == s[right]):
                left -= 1
                right +=1
                counter += 1
            return counter
        counter = 0
        
        for i in range(len(s)):
            len1 = expandFromMiddle(s, i, i)
            len2 = expandFromMiddle(s, i, i + 1)
            counter += len1 + len2
        return counter
```
- Pacific Atlantic Water Flow