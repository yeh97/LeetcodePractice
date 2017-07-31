

### Leetcode 48
#### [Rotate Image](https://leetcode.com/problems/rotate-image)

  

##### ***Problem:***

    You are given an n x n 2D matrix representing an image.

    Rotate the image by 90 degrees (clockwise).

##### ***Note:***
    1) clockwise rotate
    2) do this in-place
    
    
##### ***Example:***

    Input: [[1,2], [3,4]]
        Output: [[3,1], [4,2]]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_31
 *Language: Java
 *
 */

public class Solution {
    public void rotate(int[][] matrix) {
        //rotate group
        //[i,j], [j,n-1-i], [n-1-j,i], [n-1-i,n-1-j]
        if (matrix == null || matrix.length == 0) return;
        if (matrix.length != matrix[0].length) return;
        int n = matrix.length;
        int rowend = n / 2;
        int colend = (n + 1) / 2;
        for (int i = 0; i < rowend; i++) {
            for (int j = 0; j < colend; j++) {
                //clockwise
                rotate(matrix, n-1-j, i, n-1-i, n-1-j, j, n-1-i, i, j);
            }
        }
    }
    private void rotate(int[][] n, int x1, int y1, int x2, 
                        int y2, int x3, int y3, int x4, int y4) {
        int t = n[x1][y1];
        n[x1][y1] = n[x2][y2];
        n[x2][y2] = n[x3][y3];
        n[x3][y3] = n[x4][y4];
        n[x4][y4] = t;
    }
}

```

