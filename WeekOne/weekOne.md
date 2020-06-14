## Week 1 - Sequences
In week 1, we will start off easy and do a mix of easy and medium questions on arrays and strings. 
Arrays and strings are the most common types of questions to be found in interviews; gaining familiarity with them will help in building strong fundamentals to better handle tougher questions.


-  [Two Sum](https://leetcode.com/problems/two-sum)
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dicte = {}
        for idx, num in enumerate(nums):
            remaining = target - num
            if remaining in dicte:
                return (dicte[remaining], idx)
            else:
                dicte[num] = idx
```


-  [Contains Duplicate](https://leetcode.com/problems/contains-duplicate)

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        set_nums = set()
        for i in nums:
            if i in set_nums:
                return True
            else:
                set_nums.add(i)
        return False
```

- [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if prices == []:
            return 0
        low = prices[0]
        max_profit = 0
        for i in range(1, len(prices)):
            if prices[i] < low:
                low = prices[i]
            else:
                profit = prices[i] - low
                if profit > max_profit:
                    max_profit = profit
        return max_profit
                
```


- [Valid Anagram](https://leetcode.com/problems/valid-anagram/)

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return collections.Counter(s) == collections.Counter(t)
```


- [Valid Parentheses](https://leetcode.com/problems/valid-anagram)
```python
class Solution:
    def isValid(self, s: str) -> bool:
        dicte = {"[":"]", "{":"}", "(": ")"}
        openBrac = {"[", "{", "("}
        stack = []
        for i in range(len(s)):
            if s[i] in openBrac:
                stack.append(s[i])
            else:
                if len(stack) == 0:
                    return False
                popper = stack.pop()
                if dicte[popper] != s[i]:
                    return False
        return len(stack) == 0
```

- [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self)
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        arr = [1]
        
        # Multiply with everything before
        for i in range(0, len(nums) - 1):
            arr.append(arr[i] * nums[i])
        print(arr)
        r = 1
        
        #Multiply with everything after
        for j in range(len(nums) - 1, -1, -1):
            arr[j] = arr[j] * r
            r = r * nums[j]
        
        return arr
```


- [Maximum Subarray](https://leetcode.com/problems/maximum-subarray)

    - Divide and Conquer Approach
    ```python
  class Solution:
    def maxSubArray(self, nums):

        def divide_and_conquer(nums, i, j):
            if i == j -1:
                return nums[i], nums[i], nums[i], nums[i]
            
            mid = i + (j - i) // 2
            
            
            left_1, mid_1, right_1, whole_1 = divide_and_conquer(nums, i, mid)
            left_2, mid_2, right_2, whole_2 = divide_and_conquer(nums, mid, j)
            
            
            left = max(left_1, whole_1 + left_2)
            mid = max(mid_1, mid_2, right_1 + left_2)
            right = max(right_2, whole_2 + right_1)
            whole = whole_1 + whole_2
            
            
            return left, mid, right, whole
        _, mid, _, _ = divide_and_conquer(nums, 0, len(nums))
        return mid
   ```
    - Iterative Approach
    ```python
      class Solution:
          def maxSubArray(self, nums):
            curSum = maxSum = nums[0]
            for i in range(1, len(nums)):
                num = nums[i] 
                curSum = max(num, curSum + num)
                maxSum = max(maxSum, curSum)
            return maxSum     
  ```  

- 3Sum

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        numSet = set(nums)
        numCount = collections.Counter(nums)
        posSet = {num for num in numSet if num > 0}
        negSet = {num for num in numSet if num < 0}
        finalSet = set()
        if numCount[0] >= 3:
            finalSet.add((0,0,0))
        for pos in posSet:
            for neg in negSet:
                diff = (pos + neg) * -1
                if diff in numSet:
                    val = (pos, neg, diff)
                    if val.count(pos) <= numCount[pos] and val.count(neg) <= numCount[neg] and val.count(diff) <= numCount[diff]:
                        finalSet.add(tuple(sorted(list(val))))
        return finalSet
            
```

- [Merge Intervals](https://leetcode.com/problems/merge-intervals/submissions/)

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        
        intervals.sort()
        merged = []
        
        for inter in intervals:
            if not merged or inter[0] > merged[-1][1]:
                merged.append(inter)
            else:
                merged[-1][1] = max(merged[-1][1], inter[1])
        return merged
        
```
- [Group Anagrams](https://leetcode.com/problems/group-anagrams/submissions/)

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        d = {}
        for stri in strs:
            key = tuple(sorted(stri))
            d[key] = d.get(key, []) + [stri]
        return d.values()


```
