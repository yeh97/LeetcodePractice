

### Leetcode 85
#### [Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle)

  

##### ***Problem:***

    Given a 2D binary matrix filled with 0's and 1's, 
    find the largest rectangle containing only 1's and return its area.

##### ***Example:***


    Input: [[1, 0, 1, 0, 0], 
            [1, 0, 1, 1, 1], 
            [1, 1, 1, 1, 1], 
            [1, 0, 0, 1, 0]]
        Output: 6

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_08
 *Language: Java
 *
 */

public class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix == null || matrix.length == 0) return 0;
        if (matrix[0] == null || matrix[0].length == 0) return 0;
        //height[i][j] == k <--> m[i][j] .. m[i - k + 1][j] == 1
        int[][] height = new int[matrix.length][matrix[0].length];
        for (int j = 0; j < matrix[0].length; j++) {
            if (matrix[0][j] == '1') height[0][j] = 1;
        }
        for (int i = 1; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] == '1') height[i][j] = height[i - 1][j] + 1;
                else height[i][j] = 0;
            }
        }
        int maxArea = 0;
        for (int i = 0; i < matrix.length; i++) {
            maxArea = Math.max(maxArea, largestRectangleArea(height[i]));
        }
        return maxArea;
    }
    //leetcode 84
    public int largestRectangleArea(int[] heights) {
        if (heights == null || heights.length == 0) return 0;
        int[] lborder = new int[heights.length];
        int[] rborder = new int[heights.length];
        //l[i] < i, h[l[i]] < h[i], h[l[i] + 1] >= h[i], or l[i] == -1
        //r[i] > i, h[r[i]] < h[i], h[r[i] - 1] >= h[i], or r[i] == n
        //if rectangle contain whole h[i]
        //j in (l[i], r[i]), h[j] belong to this rectangle
        //area is h[i] * (r[i] - l[i] - 1)
        lborder[0] = -1;
        for (int i = 1; i < heights.length; i++) {
            int l = i - 1;
            while (l >= 0 && heights[i] <= heights[l]) {
                l = lborder[l];
            }
            lborder[i] = l;
        }
        rborder[heights.length - 1] = heights.length;
        for (int i = heights.length - 2; i >= 0; i--) {
            int r = i + 1;
            while (r < heights.length && heights[i] <= heights[r]) {
                r = rborder[r];
            }
            rborder[i] = r;
        }
        int maxArea = 0;
        for (int i = 0; i < heights.length; i++) {
            //currentArea = heights[i] * (rborder[i] - lborder[i] - 1)
            maxArea = Math.max(maxArea, heights[i] * (rborder[i] - lborder[i] - 1));
        }
        return maxArea;
    }
}

```


