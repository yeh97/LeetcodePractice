

### Leetcode 120
#### [Triangle](https://leetcode.com/problems/triangle)

  

##### ***Problem:***

    Given a triangle, 
    find the minimum path sum from top to bottom. 
    
    Each step you may move to adjacent numbers on the row below.
    

##### ***Example:***

    Input: [[1],[2,3]]
        Output: 3

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_15
 *Language: Java
 *
 */

public class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        // dp[i][j] : min from dp[0][0]
        int n = triangle.size();
        int[][] dp = new int[n][n];
        dp[0][0] = triangle.get(0).get(0);
        for (int i = 1; i < n; i++) {
            List<Integer> curList = triangle.get(i);
            dp[i][0] = curList.get(0) + dp[i - 1][0];
            for (int j = 1; j < i; j++) {
                dp[i][j] = curList.get(j);
                dp[i][j] += Math.min(dp[i - 1][j], dp[i - 1][j - 1]);
            }
            dp[i][i] = curList.get(i) + dp[i - 1][i - 1];
        }
        return getMin(dp[n - 1]);
    }
    private int getMin(int[] nums) {
        int min = nums[0];
        for (int i = 1; i < nums.length; i++) {
            min = Math.min(min, nums[i]);
        }
        return min;
    }
}


```


