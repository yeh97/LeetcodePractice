

### Leetcode 153
#### [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array)

  

##### ***Problem:***

    Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
    Find the minimum element.
    You may assume no duplicate exists in the array.
    
##### ***Example:***

    Input: [4,5,6,7,0,1,2]
        Output: 0


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_01_30
 *Language: Java
 *
 */

class Solution {
    public int findMin(int[] nums) {
        // 2018/1/30 : 0ms
        if (nums == null || nums.length == 0) return 0;
        int l = 0;
        int r = nums.length - 1;
        while (l < r) {
            int m = l + (r - l) / 2;
            if (nums[m] > nums[r]) {
                // rotated center in m+1...r
                // --> min(nums) in nums[m+1...r]
                l = m + 1;
            } else {
                // rotated center in l...m
                // --> min(nums) in nums[l...m]
                r = m;
            }
        }
        return nums[l];
    }
}

```
