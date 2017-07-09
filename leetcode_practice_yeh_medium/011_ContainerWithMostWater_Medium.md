

### Leetcode 11
#### [Container With Most Water](https://leetcode.com/problems/container-with-most-water)
  
    Given n non-negative integers a[1], a[2], ..., a[n], 
    where each represents a point at coordinate (i, a[i]).
    
    n vertical lines are drawn such that 
    the two endpoints of line i is at (i, a[i]) and (i, 0). 
    
    Find two lines, 
    which together with x-axis forms a container, 
    such that the container contains the most water.

**Note:**

    You may not slant the container and n is at least 2.
    

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_09
 *Language: Java
 *
 */

public class Solution {
    public int maxArea(int[] height) {
        if(height==null || height.length<2) return 0;
        int l = 0;
        int r = height.length-1;
        //the maxArea needed return
        int ret = 0;
        int nextpoint;
        while(r>l) {
            //Area = (r-l)*Math.min(height[l], height[r]);
            ret = Math.max((r-l)*Math.min(height[l], height[r]), ret);
            if(height[l]<height[r]) {
                //if next num not bigger than this, Area must be smaller
                //so get next left bigger than this
                nextpoint = l;
                while(nextpoint<r && height[nextpoint]<=height[l]){
                    nextpoint++;
                }
                l = nextpoint;
            }else{
                nextpoint = r;
                while(nextpoint>l && height[nextpoint]<=height[r]){
                    nextpoint--;
                }
                r = nextpoint;
            }
        }
        return ret;
    }
}

```
