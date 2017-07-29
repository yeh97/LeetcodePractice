

### Leetcode 42
#### [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water)

  

##### ***Problem:***

    Given n non-negative integers representing an elevation map 
    where the width of each bar is 1, 
    compute how much water it is able to trap after raining.
    
##### ***Example:***

    Input: [0,1,0,2,1,0,1,3,2,1,2,1]
        Output: 6
![ImageHeight](http://www.leetcode.com/static/images/problemset/rainwatertrap.png)

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_29
 *Language: Java
 *
 */

public class Solution {
    public int trap(int[] height) {
        if (height==null || height.length==0) return 0;
        //2D : two pointers
        //3D : priority query (heap)
        int l = 0;
        int r = height.length - 1;
        //lval : max of nums[0...l]
        //rval : max of nums[r...nums.length-1]
        int lval = height[l];
        int rval = height[r];
        int ret = 0;
        while (l < r) {
            if (lval < rval) {
                l++;
                if (lval > height[l]) {
                    ret += lval - height[l];
                } else {
                    lval = height[l];
                }
            } else {
                r--;
                if (rval > height[r]) {
                    ret += rval - height[r];
                } else {
                    rval = height[r];
                }
            }
        }
        return ret;
    }
}

```

