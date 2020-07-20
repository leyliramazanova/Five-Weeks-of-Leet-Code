

- [Count Primes](https://leetcode.com/problems/count-primes/submissions/)
```python
class Solution:
    def countPrimes(self, n: int) -> int:
        s = set()
        for i in range(2, n):
            s.add(i)
        for i in range(2, n):
            if i not in s:
                continuea
            s = self.filterMultiples( s, i)
        return len(s)
                    
    def filterMultiples(self, seti, element):
        new_s = set()
        new_s.add(element)
        for el in seti:
            if el % element != 0:
                new_s.add(el)
        # print(new_s)
        return new_s
``` 
            
        
