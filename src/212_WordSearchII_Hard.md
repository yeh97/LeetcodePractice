


### Leetcode 212
#### [Word Search II](https://leetcode.com/problems/word-search-ii)

  

##### ***Problem:***
    Given a 2D board and a list of words from the dictionary, find all words in the board.
    Each word must be constructed from letters of sequentially adjacent cell,
    where "adjacent" cells are those horizontally or vertically neighboring.
    The same letter cell may not be used more than once in a word.

##### ***Example:***

    Input: [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]]
            ["oath","pea","eat","rain"]
        Output: ["eat","oath"]


##### *Method #1*
``` python3
/*
 *Author: yeh
 *Time: 2018_07_04
 *Language: Python3
 *
 */

class Solution:
    def makeTrie(self, words):
        """Leetcode 208"""
        def insert(word, trieNode):
            cur = trieNode
            for letter in word:
                if letter not in cur:
                    cur[letter] = {}
                cur = cur[letter]
            cur["end"] = True
        trie = {}
        for word in words:
            insert(word, trie)
        return trie
            
    def findWords(self, board, words):
        """
        :type board: List[List[str]]
        :type words: List[str]
        :rtype: List[str]
        """
        wordTrie = self.makeTrie(words)
        # size(board, m * n) > 0
        m, n = len(board), len(board[0])
        visited, res = [[False] * n for _ in range(m)], []
        
        def DFS(x, y, word, trieNode):
            if x < 0 or x >= m or y < 0 or y >= n or visited[x][y]:
                return
            if board[x][y] in trieNode:
                trieNode = trieNode[board[x][y]]
                word += board[x][y]
                if "end" in trieNode:
                    res.append(word)
                    trieNode.pop("end")
                visited[x][y] = True
                DFS(x + 1, y, word, trieNode)
                DFS(x - 1, y, word, trieNode)
                DFS(x, y + 1, word, trieNode)
                DFS(x, y - 1, word, trieNode)
                visited[x][y] = False
        
        for ii in range(m):
            for jj in range(n):
                DFS(ii, jj, '', wordTrie)
        # delete duplicate elements
        return res

```





