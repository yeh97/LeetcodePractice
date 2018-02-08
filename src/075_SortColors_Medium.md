

### Leetcode 75
#### [Sort Colors](https://leetcode.com/problems/sort-colors)

  

##### ***Problem:***

    Given an array with n objects colored red, white or blue, 
    sort them so that objects of the same color are adjacent, 
    with the colors in the order red, white and blue.

    Here, we will use the integers 0, 1, and 2 to 
    represent the color red, white, and blue respectively.
    
##### ***Example:***

    Input: [2,1,1,0,2]
        Output: [0,1,1,2,2]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_07
 *Language: Java
 *
 */

public class Solution {
    public void sortColors(int[] nums) {
        if (nums == null || nums.length == 0) return;
        int rNum = 0;
        int wNum = 0;
        //int bNum = 0;
        for (int color : nums) {
            if (color == 0) rNum++;
            else if (color == 1) wNum++;
            //else bNum++;//color == 2
        }
        for (int i = 0; i < rNum; i++) {
            nums[i] = 0;
        }
        for (int i = 0; i < wNum; i++) {
            nums[i + rNum] = 1;
        }
        for (int i = rNum + wNum; i < nums.length; i++) {
            nums[i] = 2;
        }
    }
}
```
