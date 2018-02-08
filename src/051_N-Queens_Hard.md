

### Leetcode 51
#### [N-Queens](https://leetcode.com/problems/n-queens)

  

##### ***Problem:***

    The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.
    
![ImageNQueens](https://leetcode.com/static/images/problemset/8-queens.png)

    Given an integer n, return all distinct solutions to the n-queens puzzle.

    Each solution contains a distinct board configuration of the n-queens' placement, 
    where 'Q' and '.' both indicate a queen and an empty space respectively.
    
    
##### ***Example:***

    Input: 1
        Output: [["Q"]]
    Input: 3
        Output: []

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_01
 *Language: Java
 *
 */

public class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ret = new ArrayList<List<String>>();
        //(i, j) : row : i, col : j
        //main diagonal : i + j, another : n - 1 - i + j
        char[][] queens = new char[n][n];
        for (char[] chs : queens) {
            Arrays.fill(chs, '.');
        }
        solveNQueensDFS(ret, queens, n, 0, new boolean[n], new boolean[n],
                       new boolean[2 * n - 1], new boolean[2 * n - 1]);
        return ret;
    }
    private void solveNQueensDFS(List<List<String>> list, char[][] queens, int n,
                                 int step, boolean[] rowused, boolean[] colused, 
                                 boolean[] mdiagused, boolean[] adiagused) {
        if (step >= n) {
            List<String> solution = new ArrayList<String>();
            for (int i = 0; i < queens.length; i++) {
                solution.add(new String(queens[i]));
            }
            list.add(solution);
        } else {
            for (int i = 0; i < queens[step].length; i++) {
                if (rowused[step] || colused[i]) continue;
                if (mdiagused[i + step] || adiagused[n - 1 - step + i]) continue;
                rowused[step] = colused[i] = true;
                mdiagused[i + step] = adiagused[n - 1 - step + i] = true;
                queens[step][i] = 'Q';
                solveNQueensDFS(list, queens, n, step + 1, 
                               rowused, colused, mdiagused, adiagused);
                rowused[step] = colused[i] = false;
                mdiagused[i + step] = adiagused[n - 1 - step + i] = false;
                queens[step][i] = '.';
            }
        }
    }
}

```


