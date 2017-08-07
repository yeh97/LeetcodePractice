

### Leetcode 73
#### [Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes)

  

##### ***Problem:***

    Given a m x n matrix, if an element is 0, 
    set its entire row and column to 0. Do it in place.
    
##### ***Note:***

    1) set all element of the row and col contain zero to 0
    2) matrix[m][n], m, n may be 0
    
##### ***Example:***

    Input: [[0,1], [1,1]]
        Output: [[0,0], [0,1]]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_07
 *Language: Java
 *
 */

public class Solution {
    public void setZeroes(int[][] matrix) {
        if (matrix == null) return;
        if (matrix.length == 0 || matrix[0].length == 0) return;
        boolean[] rowZero = new boolean[matrix.length];
        boolean[] colZero = new boolean[matrix[0].length];
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] == 0) {
                    rowZero[i] = colZero[j] = true;
                }
            }
        }
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (rowZero[i] || colZero[j]) {
                    matrix[i][j] = 0;
                }
            }
        }
    }
}
```

