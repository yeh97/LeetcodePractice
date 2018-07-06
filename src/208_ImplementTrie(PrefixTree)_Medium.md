


### Leetcode 208
#### [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree)


##### ***Problem:***

    Implement a trie with insert, search, and startsWith methods.

##### ***Example:***

    Input: ["Trie","insert","search","search","startsWith","insert","search"]
            [[],["apple"],["apple"],["app"],["app"],["app"],["app"]]
        Output: [null,null,true,false,true,null,true]

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_03
 *Language: Python3
 *
 */

class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.val = {}

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: void
        """
        cur = self.val
        for letter in word:
            if letter not in cur:
                cur[letter] = {}
            cur = cur[letter]
        cur["end"] = True

    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        cur = self.val
        for letter in word:
            if letter not in cur:
                return False
            cur = cur[letter]
        return "end" in cur

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        cur = self.val
        for letter in prefix:
            if letter not in cur:
                return False
            cur = cur[letter]
        return True

```

