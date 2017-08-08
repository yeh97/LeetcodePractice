

### Leetcode 84
#### [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram)

  

##### ***Problem:***

    Given n non-negative integers representing the histogram's bar height 
    where the width of each bar is 1, 
    find the area of largest rectangle in the histogram.

##### ***Example:***

![ImageInput](https://leetcode.com/static/images/problemset/histogram.png)

    Input: [2,1,5,6,2,3]

![ImageOutput](https://leetcode.com/static/images/problemset/histogram_area.png)

        Output: 10

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_08
 *Language: Java
 *
 */

public class Solution {
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


