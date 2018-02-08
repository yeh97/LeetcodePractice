

### Leetcode 79
#### [Word Search](https://leetcode.com/problems/word-search)

  

##### ***Problem:***

    Given a 2D board and a word, 
    find if the word exists in the grid.

    The word can be constructed from letters of sequentially adjacent cell,
    where "adjacent" cells are those horizontally or vertically neighboring. 
    The same letter cell may not be used more than once.


##### ***Example:***

    Input: [ ['A','B','C','E'], ['S','F','C','S'], 
            ['A','D','E','E'] ], "ABC"
        Output: true

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_08
 *Language: Java
 *
 */

public class Solution {
    public boolean exist(char[][] board, String word) {
        if (board == null || board.length == 0) return false;
        if (board[0] == null || board[0].length == 0) return false;
        if (word == null || word.length() == 0) return false;
        boolean[][] used = new boolean[board.length][board[0].length];
        char[] chsWord = word.toCharArray();
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (existDFS(board, used, chsWord, 0, i, j)) {
                    return true;
                }
            }
        }
        return false;
    }
    private boolean existDFS(char[][] board, boolean[][] used, 
                             char[] word, int index, int row, int col) {
        if (index == word.length) return true;
        if (row < 0 || col < 0 || row >= board.length || col >= board[0].length) return false;
        if (used[row][col] || word[index] != board[row][col]) return false;
        used[row][col] = true;
        boolean ret = 
            existDFS(board, used, word, index + 1, row, col - 1) // toL
            || existDFS(board, used, word, index + 1, row, col + 1) // toR
            || existDFS(board, used, word, index + 1, row - 1, col) // toU
            || existDFS(board, used, word, index + 1, row + 1, col); // toD
        used[row][col] = false;
        return ret;
    }
}

```


