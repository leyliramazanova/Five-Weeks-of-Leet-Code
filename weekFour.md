## Week 4 - More Data Structures#

<p>Week 4 builds up on knowledge from previous weeks but questions are of increased difficulty. Expect to see such level of questions during interviews. You get more practice on more advanced data structures such as (but not exclusively limited to) heaps and tries.
</p>

- [Add and Search Word](https://leetcode.com/problems/add-and-search-word-data-structure-design/discuss/714044/Fast-Short-Python-Trie-Solution-explained)
	
	```python
		class TrieNode:
		    def __init__(self):
			self.trie = {}
			self.terminating = False

		class WordDictionary:

		    def __init__(self):
			"""
			Initialize your data structure here.
			"""
			self.trieNode = TrieNode()


		    def addWord(self, word: str) -> None:
			"""
			Adds a word into the data structure.
			"""

			cur_trie = self.trieNode
			for i in range(len(word)):
			    char = word[i]

			    if char not in cur_trie.trie:
				cur_trie.trie[char] = TrieNode()
				cur_trie = cur_trie.trie[char]
			    else:
				cur_trie = cur_trie.trie[char]

			cur_trie.terminating = True



		    def search(self, word: str) -> bool:
			"""
			Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
			"""    
			def _search(subWord, trieNode):
			    if not subWord:
				return trieNode.terminating 

			    if not trieNode.trie:
				return False

			    if subWord[0] in trieNode.trie:
				return _search(subWord[1:], trieNode.trie[subWord[0]])
			    elif subWord[0] == '.':
				for ch in trieNode.trie.keys():
				    if _search(subWord[1:], trieNode.trie[ch]):
					return True
			    return False

			return _search(word, self.trieNode)
	```
- [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/)

	```python
		class TrieNode:
		    def __init__(self):
			self.trie = {}
			self.terminating = False

		class Trie:

		    def __init__(self):
			"""
			Initialize your data structure here.
			"""
			self.trieNode = TrieNode()


		    def insert(self, word: str) -> None:
			"""
			Inserts a word into the trie.
			"""
			cur_trie = self.trieNode
			for char in word:
			    if char not in cur_trie.trie:
				cur_trie.trie[char] = TrieNode()
				cur_trie = cur_trie.trie[char]
			    else:
				cur_trie = cur_trie.trie[char]
			cur_trie.terminating = True




		    def search(self, word: str) -> bool:
			"""
			Returns if the word is in the trie.
			"""
			cur_trie = self.trieNode
			for char in word:
			    if char in cur_trie.trie:
				cur_trie = cur_trie.trie[char]
			    else:
				return False
			return cur_trie.terminating 


		    def startsWith(self, prefix: str) -> bool:
			"""
			Returns if there is any word in the trie that starts with the given prefix.
			"""
			cur_trie = self.trieNode
			for char in prefix:
			    if char in cur_trie.trie:
				cur_trie = cur_trie.trie[char]
			    else:
				return False
			return True
	```
- [Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/submissions/)

	```python
	class Solution:
	    def isSametree(self, s, t):
		if not s and not t:
		    return True
		if (not s or not t):
		    return False

		return s.val == t.val and self.isSametree(s.left,t.left) & self.isSametree(s.right,t.right)


	    def isSubtree(self, s: TreeNode, t: TreeNode) -> bool:
		if not s:
		    return False
		if self.isSametree(s,t):
		    return True
		return self.isSubtree(s.left, t) or self.isSubtree(s.right, t) 
	```

- [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/submissions/)

	```python
	class Solution:
	    def traverse(self, liste, node):
		    if node.left:
			self.traverse(liste, node.left)
		    liste.append(node.val)
		    if node.right:
			self.traverse(liste, node.right)

	    def kthSmallest(self, root: TreeNode, k: int) -> int:
		l = []
		self.traverse(l, root)
		return l[k - 1]
	```
- [Lowest Common Ancestor of BST](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
	- Recursive
	```python
		class Solution:
		    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
			p_val = p.val
			q_val = q.val

			root_val = root.val

			if p_val > root_val and q_val > root_val:
			    return self.lowestCommonAncestor(root.right, p, q)

			if p_val < root_val and q_val < root_val:
			    return self.lowestCommonAncestor(root.left, p, q)

			else:
			    return root
	```
	
	- Iterative
	```python
	class Solution:
    	    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
		p_val = p.val
		q_val = q.val

		while root:

		    root_val = root.val

		    if p_val > root_val and q_val > root_val:
			root = root.right
		    elif p_val < root_val and q_val < root_val:
			root = root.left
		    else:
			return root
	```
- Merge K Sorted Lists
	- Brute Force Approach
	```python
		class Solution:
		    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
			bigList = []
			for l in lists:
			    while l != None:
				bigList.append(l.val)
				l = l.next 
			bigList = sorted(bigList)
			node = None
			nodeCopy = None
			for val in bigList:
			    if not node:
				node = ListNode(val)
				nodeCopy = node
			    else:
				node.next = ListNode(val)
				node = node.next
			return nodeCopy
	```
- Find Median from Data Stream
- Insert Interval

- [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/submissions/)
	- Brute Force
	```python
	class Solution:
	    def longestConsecutive(self, nums: List[int]) -> int:
		numSet = set(nums)
		longestStreak = 0
		for num in nums:
		    curNum = num + 1
		    longest = 1
		    while curNum in numSet:
			curNum += 1
			longest += 1
		    longestStreak = max(longest, longestStreak)
		return longestStreak
	```
- Word Search II
