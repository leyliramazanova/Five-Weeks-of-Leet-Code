## More questions

- [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/submissions/)

```python
    # Definition for a binary tree node.
    # class TreeNode:
    #     def __init__(self, val=0, left=None, right=None):
    #         self.val = val
    #         self.left = left
    #         self.right = right
    class Solution:

        def height(self, root):
            if not root:
                return 0
            return max(self.height(root.left), self.height(root.right)) + 1

        def isBalanced(self, root: TreeNode) -> bool:
            if not root:
                return True
            lh = self.height(root.left)
            rh = self.height(root.right)

            return abs(lh - rh) <= 1 and self.isBalanced(root.left) and self.isBalanced(root.right)
```
