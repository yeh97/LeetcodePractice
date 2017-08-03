

### Leetcode 63
#### [Unique Paths II](https://leetcode.com/problems/unique-paths-ii)

  

##### ***Problem:***

    Follow up for "Unique Paths":
    Now consider if some obstacles are added to the grids.
    How many unique paths would there be?
    An obstacle and empty space is marked as 1 and 0 respectively in the grid.
    (1 : obstacle)
    
##### ***Note:***

    1) m, n <= 100
    
##### ***Example:***

    Input: [[0,1], [0,0]]
        Output: 1


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_03
 *Language: Java
 *
 */

public class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid == null) return 0;
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        //has no data
        if (m == 0 || n == 0) return 0;
        //can't Start or can't Finish
        if (obstacleGrid[0][0] == 1 || obstacleGrid[m - 1][n - 1] == 1) return 0;
        int[][] dp = new int[m][n];
        for (int i = 0; i < m; i++) {
            if (obstacleGrid[i][0] == 1) break;
            dp[i][0] = 1;
        }
        for (int j = 0; j < n; j++) {
            if (obstacleGrid[0][j] == 1) break;
            dp[0][j] = 1;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (obstacleGrid[i][j] == 0) dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
}

```

