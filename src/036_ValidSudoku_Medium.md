

### Leetcode 36
#### [Valid Sudoku](https://leetcode.com/problems/valid-sudoku)

  

##### ***Problem:***

    Determine if a Sudoku is valid, according to:  
###### *[Sudoku Puzzles-The Rules](http://sudoku.com.au/TheRules.aspx)*

    The Sudoku board could be partially filled, 
    where empty cells are filled with the character '.'.
    
    A valid Sudoku board (partially filled) is not necessarily solvable. 
    Only the filled cells need to be validated.
    
    
##### ***Example:***

![image](http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

    A partially filled sudoku which is valid.
    

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_26
 *Language: Java
 *
 */

public class Solution {
    
    public static final int sudoku_size = 9;
    public static final int sudoku_mod = 3;
    public static final char cempty = '.';
    
    public boolean isValidSudoku(char[][] board) {
        if (null == board || null == board[0]) {
            return false;
        }
        
        int legth = board.length;
        int width = board[0].length;
        if (legth != sudoku_size || width != sudoku_size) {
            return false;
        }
        
        char[] smod = new char[sudoku_size];
        for (int i = 0; i < sudoku_size; i++) {
           for (int j = 0; j < sudoku_size; j++) {
               smod[j] = board[i][j];
           }
           if (isvalidmod(smod) == false) {
               return false;
           }
        }
        for (int i = 0; i < sudoku_size; i++) {
           for (int j = 0; j < sudoku_size; j++) {
               smod[j] = board[j][i];
           }
           if (isvalidmod(smod) == false) {
               return false;
           }
        }
        for (int i = 0; i < sudoku_size; i++) {
           int r = i / sudoku_mod * sudoku_mod;
           int l = i % sudoku_mod * sudoku_mod;
           int cnt = 0;
           for (int ra = 0; ra < sudoku_mod; ra++) {
               for (int la = 0; la < sudoku_mod; la++) {
                   smod[cnt] = board[r + ra][l + la];
                   cnt++;
               }
           }
           if(isvalidmod(smod) == false) {
               return false;
           }
        }
        return true;
    }
    public boolean isvalidmod(char[] src) {
        if (null == src || src.length != sudoku_size) {
            return false;
        }
        
        HashMap<Character,Boolean> map = new HashMap<Character,Boolean>();
        for (char c:src) {
            if (c==cempty) continue;
            if (map.containsKey(c) == true) {
                return false;
            } else {
                map.put(c,true);
            }
        }
        return true;
    }
}

```

