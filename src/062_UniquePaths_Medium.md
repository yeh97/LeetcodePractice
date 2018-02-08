

### Leetcode 62
#### [Unique Paths](https://leetcode.com/problems/unique-paths)

  

##### ***Problem:***

    A robot is located at the top-left corner of a m x n grid 
    (marked 'Start' in the diagram below).
    The robot can only move either down or right at any point in time. 
    The robot is trying to reach the bottom-right corner of the grid 
    (marked 'Finish' in the diagram below).
    How many possible unique paths are there?
![ImageRobotUniquePaths](https://leetcode.com/static/images/problemset/robot_maze.png)
    
##### ***Note:***

    1) m, n <= 100
    
##### ***Example:***

    Input: 9, 2
        Output: 9


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_03
 *Language: Java
 *
 */

public class Solution {
    public int uniquePaths(int m, int n) {
        if (m <= 0 || n <= 0) return 0;
        int[][] dp = new int[m][n];
        for (int i = 0; i < m; i++) {
            dp[i][0] = 1;
        }
        for (int j = 0; j < n; j++) {
            dp[0][j] = 1;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
}

```

