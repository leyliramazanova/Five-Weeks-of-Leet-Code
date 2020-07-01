## Week 4 - More Data Structures#

<p>Week 4 builds up on knowledge from previous weeks but questions are of increased difficulty. Expect to see such level of questions during interviews. You get more practice on more advanced data structures such as (but not exclusively limited to) heaps and tries.
</p>

- [Add and Search Word](https://leetcode.com/problems/add-and-search-word-data-structure-design/discuss/714044/Fast-Short-Python-Trie-Solution-explained)
Step 1: We initialize a trie Node, which is composed of  a dictionary and a data-structure defining if it is a terminating node.
```
class TrieNode:
    def __init__(self):
        self.trie = {}
        self.terminating = False
```

Step 2: After initiliizing a trie Node, we add characters to the TrieTree. Every time we add a complete word, the next empty dictionary that the trie references will set the terminating status to True.
```
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
```

Step 3: 
	- We search recursively. If the subword we are searching for has ended, we check for terminating condition to see if the string is present.
	- If trieNode.trie (i.e. dictionary) does not exist, it means that the subword is longer and we return False
	- If the subword's first string is in our trie dict, then we search for the second letter of the subword inside the a dict referenced by the first dict and so on 
	- If the sub-word's first character is a ".", then we search for th next word in all the possible keys in the trie node recursively
	- If the subword's character does not match the keys inside out trie node, we return False

```
        
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
- Implement Trie (Prefix Tree)
- Subtree of Another Tree
- Kth Smallest Element in a BST
- Lowest Common Ancestor of BST
- Merge K Sorted Lists
- Find Median from Data Stream
- Insert Interval
- Longest Consecutive Sequence
- Word Search II
