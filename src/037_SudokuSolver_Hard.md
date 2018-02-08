

### Leetcode 37
#### [Sudoku Solver](https://leetcode.com/problems/sudoku-solver)

  

##### ***Problem:***

    Write a program to solve a Sudoku puzzle by filling the empty cells.

    Empty cells are indicated by the character '.'.
    
##### ***Example:***

    Input: 
![Imageinput#1](http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

        Ouput:
![Imageouput#1](http://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)

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
    
    private char[][] board = null;
    
    private Set<Character> [] rowset = new HashSet[sudoku_size];
    private Set<Character> [] colset = new HashSet[sudoku_size];
    private Set<Character> [] blockset = new HashSet[sudoku_size];
    
    public void solveSudoku(char[][] board) {
        this.board = board;
        if (fillSet() == 0) {
            helpsolve(0, 0);
        }
    }
    //NOT valid sudoku : return -1
    //valid sudoku : return 0
    private int fillSet() {
        for (int i = 0; i < sudoku_size; i++) {
            rowset[i] = new HashSet<Character>();
            colset[i] = new HashSet<Character>();
            blockset[i] = new HashSet<Character>();
        }
        for (int i = 0; i < sudoku_size; i++) {
            for (int j = 0; j < sudoku_size; j++) {
                if (board[i][j] == cempty) continue;
                if (rowset[i].contains(board[i][j])) {
                    return -1;
                } else {
                    rowset[i].add(board[i][j]);
                }
            }
        }
        for (int i = 0; i < sudoku_size; i++) {
            for (int j = 0; j < sudoku_size; j++) {
                if (board[i][j] == cempty) continue;
                if (colset[j].contains(board[i][j])) {
                    return -1;
                } else {
                    colset[j].add(board[i][j]);
                }
            }
        }
        for (int i = 0; i< sudoku_size; i++) {
            int r = i / sudoku_mod * sudoku_mod;
            int l = i % sudoku_mod * sudoku_mod;
            for (int rr = 0; rr < sudoku_mod; rr++) {
                for (int ll = 0; ll < sudoku_mod; ll++) {
                    if (board[r + rr][l + ll] == cempty) continue;
                    if (blockset[i].contains(board[r + rr][l + ll])) {
                        return -1;
                    } else {
                        blockset[i].add(board[r + rr][l + ll]);
                    }
                }
            }
        }
        return 0;
    }
    //(board[row][col] = ch) is valid ?
    private boolean addvalid(int row, int col, char ch) {
        return !(rowset[row].contains(ch) || colset[col].contains(ch) || 
                 blockset[row / sudoku_mod * sudoku_mod + col / sudoku_mod].contains(ch));
    }
    private void add(int row, int col, char ch) {
        board[row][col] = ch;
        rowset[row].add(ch);
        colset[col].add(ch);
        blockset[row / sudoku_mod * sudoku_mod + col / sudoku_mod].add(ch);
    }
    private void remove(int row, int col, char ch) {
        board[row][col] = cempty;
        rowset[row].remove(ch);
        colset[col].remove(ch);
        blockset[row / sudoku_mod * sudoku_mod + col / sudoku_mod].remove(ch);
    }
    //DFS
    private boolean helpsolve(int row, int col) {
        if (col >= sudoku_size) {
            return helpsolve(row + 1, 0);
        }
        if (row == sudoku_size) {
            return true;
        }
        if (board[row][col] != cempty) {
            return helpsolve(row, col + 1);
        }
        for(int i = 0; i < sudoku_size;i++) {
            if(addvalid(row, col, (char)(i + '1')) == false) {
                continue;
            }
            add(row, col, (char)(i + '1'));
            if (helpsolve(row, col + 1) == true) {
                return true;
            }
            remove(row, col, (char)(i + '1'));
        }
        return false;
    }
}


```

