


### Leetcode 174
#### [Dungeon Game](https://leetcode.com/problems/dungeon-game)

  

##### ***Problem:***

	The demons had captured the princess (P) and imprisoned her in the bottom-right corner of a dungeon. 
    The dungeon consists of M x N rooms laid out in a 2D grid. 
    Our valiant knight (K) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.
	The knight has an initial health point represented by a positive integer. 
	If at any point his health point drops to 0 or below, he dies immediately.
	Some of the rooms are guarded by demons, so the knight loses health (negative integers) upon entering these rooms; 
	other rooms are either empty (0's) or contain magic orbs that increase the knight's health (positive integers).
	In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.

	Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.

##### ***Notes:***
* The knight's health has no upper bound.
* Any room can contain threats or power-ups, even the first room the knight enters and the bottom-right room where the princess is imprisoned.
##### ***Example:***

    Input: [[-2,-3,3],[-5,-10,1],[10,30,-5]]
        Output: 7


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_05
 *Language: Java
 *
 */

class Solution {
    long[][] data = null;
    long[][] cur = null;
    int m, n;
    public int calculateMinimumHP(int[][] dungeon) {
        // 2018/2/5 : 10ms
        // Binary minimunHP + dp(can survival in current HP)
        // O(lg(Long.MAX_VALUE) * M * N)
        if (dungeon == null) return 0;
        if (dungeon.length == 0 || dungeon[0].length == 0) return 0;
        this.m = dungeon.length;
        this.n = dungeon[0].length;
        this.data = new long[m][n];
        this.cur = new long[m][n];
        // copy
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                data[i][j] = (long) dungeon[i][j];
            }
        }
        long l = 1; // min hp
        long r = Long.MAX_VALUE; // > -m * n * Integer.MIN_VALUE
        while (l < r) {
            long mid = l + (r - l) / 2;
            if (rescueByCurHP(mid)) {
                // [l, mid]
                r = mid;
            } else {
                // [mid + 1, r]
                l = mid + 1;
            }
        }
        return (int) l;
    }
    private boolean rescueByCurHP(long hp) {
        // dp
        if ((cur[0][0] = data[0][0] + hp) <= 0) return false;
        for (int i = 1; i < m; i++) {
            cur[i][0] = cur[i - 1][0] > 0 ? cur[i - 1][0] + data[i][0] : -1;
        }
        for (int j = 1; j < n; j++) {
            cur[0][j] = cur[0][j - 1] > 0 ? cur[0][j - 1] + data[0][j] : -1;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                cur[i][j] = Math.max(
                    cur[i - 1][j] > 0 ? cur[i - 1][j] + data[i][j] : -1, 
                    cur[i][j - 1] > 0 ? cur[i][j - 1] + data[i][j] : -1
                );
            }
        }
        return cur[m - 1][n - 1] > 0;
    }
}


```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2018_02_05
 *Language: Java
 *
 */

class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        // 2018/2/5 : 3ms
        // dp
        if (dungeon == null) return 0;
        if (dungeon.length == 0 || dungeon[0].length == 0) return 0;
        int m = dungeon.length;
        int n = dungeon[0].length;
        // dp[i][j] : min hp from (i, j) to (m - 1, n - 1), >= 1
        // i)  if dungeon[i][j] <= 0, dp[i][j] > -dungeon[i][j]
        //     else dp[i][j] >= 1
        // ii) dp[i][j] > min(dp[i + 1][j], dp[i][j + 1])
        int[][] dp = new int[m][n];
        dp[m - 1][n - 1] = 1 - Math.min(dungeon[m - 1][n - 1], 0);
        for (int i = m - 2; i >= 0; i--) {
            dp[i][n - 1] = Math.max(dp[i + 1][n - 1] - dungeon[i][n - 1], 1);
        }
        for (int j = n - 2; j >= 0; j--) {
            dp[m - 1][j] = Math.max(dp[m - 1][j + 1] - dungeon[m - 1][j], 1);
        }
        for (int i = m - 2; i >= 0; i--) {
            for (int j = n - 2; j >= 0; j--) {
                dp[i][j] = Math.max(Math.min(dp[i + 1][j], dp[i][j + 1]) - dungeon[i][j], 1);
            }
        }
        return dp[0][0];
    }
}



```





