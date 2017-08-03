

### Leetcode 64
#### [Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum)

  

##### ***Problem:***

    Given a m x n grid filled with non-negative numbers, 
    find a path from top left to bottom right
    which minimizes the sum of all numbers along its path.
    
##### ***Note:***

    1) m, n <= 100
    2) You can only move either down or right at any point in time.
    
##### ***Example:***

    Input: [[1,1], [0,1]]
        Output: 2


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_03
 *Language: Java
 *
 */

public class Solution {
    public int minPathSum(int[][] grid) {
        if (grid == null) return 0;
        int m = grid.length;
        int n = grid[0].length;
        //has no data
        if (m == 0 || n == 0) return 0;
        int[][] dp = new int[m][n];
        dp[0][0] = grid[0][0];
        for (int i = 1; i < m; i++) {
            dp[i][0] = grid[i][0] + dp[i - 1][0];
        }
        for (int j = 1; j < n; j++) {
            dp[0][j] = grid[0][j] + dp[0][j - 1];
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
            }
        }
        return dp[m - 1][n - 1];
    }
}

```

