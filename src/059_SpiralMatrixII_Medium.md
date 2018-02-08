

### Leetcode 59
#### [Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii)

  

##### ***Problem:***

    Given an integer n, generate a square matrix filled with elements from 1 to n**2 in spiral order.
    
##### ***Note:***

    1) similar to leetcode 54 : Spiral Matrix
    2) n == 0 output []
    
##### ***Example:***

    Input: 1
        Output: [1]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_02
 *Language: Java
 *
 */

public class Solution {
    public int[][] generateMatrix(int n) {
        if (n < 0) return null;
        
        int[][] ret = new int[n][n];
        int rows = 0;
        int rowe = n;
        int cols = 0;
        int cole = n;
        int val = 1;
        while (rows < rowe && cols < cole) {
            //-->
            //...
            for (int i = cols; i < cole; i++) {
                ret[rows][i] = val++;
            }
            rows++;
            //...|
            //...v
            for (int i = rows; i < rowe; i++) {
                ret[i][cole - 1] = val++;
            }
            cole--;
            //...
            //<--
            for (int i = cole - 1; i >= cols; i--) {
                ret[rowe - 1][i] = val++;
            }
            rowe--;
            //^...
            //|...
            for (int i = rowe - 1; i >= rows; i--) {
                ret[i][cols] = val++;
            }
            cols++;
        }
        return ret;
    }
}



```

