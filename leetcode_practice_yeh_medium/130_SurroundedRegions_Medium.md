

### Leetcode 130
#### [Surrounded Regions](https://leetcode.com/problems/surrounded-regions)

  

##### ***Problem:***

    Given a 2D board containing 'X' and 'O' (the letter O), 
    capture all regions surrounded by 'X'.

    A region is captured by flipping all 'O's into 'X's in that surrounded region.

    
##### ***Example:***

    Input: [[X, X, X, X], 
            [X, O, O, X],
            [X, X, O, X],
            [X, O, X, X]]
        Output: [[X, X, X, X], 
                 [X, X, X, X],
                 [X, X, X, X],
                 [X, O, X, X]]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_23
 *Language: Java
 *
 */

class Solution {
    public void solve(char[][] board) {
        if (board == null || board.length == 0) return;
        if (board[0] == null || board[0].length == 0) return;
        // assert board[i][j] == 'X' || board[i][j] == 'O'
        int n = board.length;
        int m = board[0].length;
        Queue<Point> q = new LinkedList<Point>();
        // 'Y' : 'O' has been scannered
        for (int i = 0; i < n; i++) {
            addPoint(q, board, i, 0);
            addPoint(q, board, i, m - 1);
        }
        for (int j = 0; j < m; j++) {
            addPoint(q, board, 0, j);
            addPoint(q, board, n - 1, j);
        }
        Point cur = null;
        int curx, cury;
        while (!q.isEmpty()) {
            cur = q.remove();
            curx = cur.row;
            cury = cur.col;
            if (curx > 0) addPoint(q, board, curx - 1, cury);
            if (cury > 0) addPoint(q, board, curx, cury - 1);
            if (curx < n - 1) addPoint(q, board, curx + 1, cury);
            if (cury < m - 1) addPoint(q, board, curx, cury + 1);
        }
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (board[i][j] == 'Y') {
                    board[i][j] = 'O';
                } else {
                    board[i][j] = 'X';
                } 
            }
        }
    }
    private void addPoint(Queue<Point> q, char[][] board, int x, int y) {
        if (board[x][y] != 'O') return;
        board[x][y] = 'Y';
        q.add(new Point(x, y));
    }
}
class Point {
    public int row;
    public int col;
    public Point(int x, int y) {
        this.row = x;
        this.col = y;
    }
}

```


