# Intermediate Level Problems and Scala Questions


- [Rotate Image](https://leetcode.com/problems/rotate-image/submissions/)
  ```python
  class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        row = col = len(matrix)
        
        for i in range(row):
            for j in range(i, col):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
        
        for i in range(row):
            for j in range(col//2):
                matrix[i][j], matrix[i][-(j+1)] = matrix[i][-(j+1)], matrix[i][j]
        
        return matrix

  ```
  
  
- [Scala- happy number](https://leetcode.com/problems/happy-number/submissions/)
  ```scala
    object Solution {
      def isHappy(n: Int): Boolean = {

          def helper(x: Int, seen:Set[Int]) : Boolean = {
              if (x == 1) true 
              else if (seen.contains(x)) false
              else helper(x.toString.map(x => (math.pow(x.asDigit, 2))).sum.toInt, seen + x)
          }
          helper(n, Set())
      }
  }
  ```
  
- [Scala- Two Sum](https://leetcode.com/problems/two-sum/submissions/)
```scala
  object Solution {
    def twoSum(nums: Array[Int], target: Int): Array[Int] = {
        
        def helper(map:Map[Int, Int], index:Int):Array[Int] = {
            val current = nums(index)
            
            map.get(target - current) match {
                case None => helper(map + (current -> index), index + 1)
                case Some(index_new) => Array(index_new, index)
            }
        }
        helper(Map(), 0)   
    }
}
```

- [Scala- Insert Position](https://leetcode.com/problems/search-insert-position/submissions/)
  ```scala
  object Solution {
      def searchInsert(nums: Array[Int], target: Int): Int = {
          val leng = nums.length 
          def helper(index:Int): Int = {
              val current = nums(index)
              if (current >= target) index
              else if (index == leng - 1) leng
              else helper(index + 1)
          }
          helper(0)
      }
  }
  ```
