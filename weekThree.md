## Week 3 - Non-Linear Data Structures#

<p>The focus of week 3 is on non-linear data structures 
like trees, graphs and heaps. You should be familiar 
with the various tree traversal (in-order, pre-order, 
post-order) algorithms and graph traversal algorithms such
as breadth-first search and depth-first search. In my experience,
using more advanced graph algorithms (Dijkstra's and Floyd-Warshall)
is quite rare and usually not necessary.</p>

- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
    - Recursive Solution
        ```python
        class Solution:
          def isValidBST(self, root: TreeNode) -> bool:
            
            def helper(node, lower= float('-inf'), upper = float('inf')):
                
                if not node:
                    return True
                
                val = node.val
                
                if (val >= upper or val <= lower):
                    return False
                
                if not helper(node.right, val, upper):
                    return False
                if not helper(node.left, lower, val):
                    return False
                return True
            return(helper(root))
        ```
     - DFS Solution
- [Invert/Flip Binary Tree]()
- Non-overlapping Intervals
- Serialize and Deserialize Binary Tree
- Construct Binary Tree from Preorder and Inorder Traversal
- Top K Frequent Elements
- Clone Graph
- Course Schedule
- Binary Tree Maximum Path Sum