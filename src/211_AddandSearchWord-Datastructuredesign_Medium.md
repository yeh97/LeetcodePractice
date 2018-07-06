


### Leetcode 211
#### [Add and Search Word - Data structure design](https://leetcode.com/problems/add-and-search-word-data-structure-design)


##### ***Problem:***

    Design a data structure that supports the following two operations:
        void addWord(word)
        bool search(word)
    search(word) can search a literal word or a regular expression string containing only letters a-z or '.'.
    A '.' means it can represent any one letter.

##### ***Example:***

    Input: ["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
            [[],["bad"],["dad"],["mad"],["pad"],["bad"],[""],["b.."]]
        Output: [null,null,null,null,false,true,false,true]

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_03
 *Language: Python3
 *
 */

class WordDictionary:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.existWord = False
        self.nextSet = {}

    def addWord(self, word):
        """
        Adds a word into the data structure.
        :type word: str
        :rtype: void
        """
        cur = self
        for letter in word:
            if letter not in cur.nextSet:
                cur.nextSet[letter] = WordDictionary()
            cur = cur.nextSet[letter]
        cur.existWord = True

    def search(self, word):
        """
        Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
        :type word: str
        :rtype: bool
        """
        if word == '':
            return self.existWord
        elif word[0] == '.':
            for nextNode in self.nextSet.values():
                if nextNode.search(word[1:]):
                    return True
            return False
        else:
            return self.nextSet[word[0]].search(word[1:]) if word[0] in self.nextSet else False

```

