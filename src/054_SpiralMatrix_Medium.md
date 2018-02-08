

### Leetcode 54
#### [Spiral Matrix](https://leetcode.com/problems/spiral-matrix)

  

##### ***Problem:***

    Given a matrix of m x n elements 
    (m rows, n columns), 
    return all elements of the matrix in spiral order.
    
##### ***Note:***

    1) clockwise
    
##### ***Example:***

    Input: [ [ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8, 9 ] ]
        Output: [1,2,3,6,9,8,7,4,5]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_01
 *Language: Java
 *
 */

public class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> ret = new LinkedList<Integer>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return ret;
        }
        int direction = 0;
        int rows = 0;
        int rowe = matrix.length;
        int cols = 0;
        int cole = matrix[0].length;
        while (rows < rowe && cols < cole) {
            if (direction == 0) {
                //-->
                //...
                for (int i = cols; i < cole; i++) {
                    ret.add(matrix[rows][i]);
                }
                rows++;
            } else if (direction == 1) {
                //...|
                //...v
                for (int i = rows; i < rowe; i++) {
                    ret.add(matrix[i][cole - 1]);
                }
                cole--;
            } else if (direction == 2) {
                //...
                //<--
                for (int i = cole - 1; i >= cols; i--) {
                    ret.add(matrix[rowe - 1][i]);
                }
                rowe--;
            } else if (direction == 3) {
                //^...
                //|...
                for (int i = rowe - 1; i >= rows; i--) {
                    ret.add(matrix[i][cols]);
                }
                cols++;
            }
            direction = (direction + 1) % 4;
        }
        return ret;
    }
}

```

