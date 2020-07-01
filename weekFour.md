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

	```
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

- Kth Smallest Element in a BST
- Lowest Common Ancestor of BST
- Merge K Sorted Lists
- Find Median from Data Stream
- Insert Interval
- Longest Consecutive Sequence
- Word Search II
