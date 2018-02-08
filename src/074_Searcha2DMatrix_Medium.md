

### Leetcode 74
#### [Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix)

  

##### ***Problem:***

    Write an efficient algorithm that searches for a value in an m x n matrix. 
    This matrix has the following properties:
    1) Integers in each row are sorted from left to right.
    2) The first integer of each row is greater than the last integer of the previous row.
    
##### ***Example:***

    Input: [[0,1], [4,5]], 2
        Output: false


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_07
 *Language: Java
 *
 */

public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        //time : O(m + n)
        //because of matrix's memory limited, time is enough
        //can use bisection method to O(lg(n) + lg(m)) 
        if (matrix == null) return false;
        if (matrix.length == 0 || matrix[0] == null || matrix[0].length == 0) return false;
        int row = 0;
        int col = 0;
        while (row < matrix.length && col < matrix[0].length) {
            if (matrix[row][col] > target) return false;
            if (matrix[row][col] == target) return true;
            if (row < matrix.length - 1 && matrix[row + 1][col] <= target) {
                row++;
            } else {
                col++;
            }
        }
        return false;
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_07
 *Language: Java
 *
 */

public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        //bisection method : O(lg(n) + lg(m)) 
        if (matrix == null) return false;
        if (matrix.length == 0 || matrix[0] == null || matrix[0].length == 0) return false;
        int rowLength = matrix.length;
        int colLength = matrix[0].length;
        //serach row : m[row][0] <= target <= m[row + 1][0]
        int rowLeft = 0;
        int rowRight = rowLength - 1;
        int rowMid;
        while (rowLeft + 1 < rowRight) {
            rowMid = rowLeft + (rowRight - rowLeft) / 2;
            if (matrix[rowMid][0] == target) return true;
            else if (matrix[rowMid][0] < target) rowLeft = rowMid;
            else rowRight = rowMid;
        }
        if (rowRight < 0) rowRight = 0;
        if (rowLeft >= rowLength) rowLeft = rowLength - 1;
        if (matrix[rowRight][0] == target || matrix[rowLeft][0] == target) return true;
        //m[row][0] < target < m[row + 1][0] --> target may in m[row]
        int row = matrix[rowRight][0] > target ? rowLeft : rowRight;
        if (matrix[row][0] > target || matrix[row][colLength - 1] < target) return false;
        //serach col
        int colLeft = 0;
        int colRight = colLength - 1;
        int colMid;
        while (colLeft + 1 < colRight) {
            colMid = colLeft + (colRight - colLeft) / 2;
            if (matrix[row][colMid] == target) return true;
            else if (matrix[row][colMid] < target) colLeft = colMid;
            else colRight = colMid;
        }
        if (colRight < 0) colRight = 0;
        if (colLeft >= colLength) colLeft = colLength - 1;
        return (matrix[row][colRight] == target || matrix[row][colLeft] == target);
    }
}


```
