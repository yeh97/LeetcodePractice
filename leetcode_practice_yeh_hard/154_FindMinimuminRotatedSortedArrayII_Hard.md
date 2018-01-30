

### Leetcode 154
#### [Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii)

  

##### ***Problem:***

    Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
    Find the minimum element.
    The array may contain duplicates.
    
##### ***Example:***

    Input: [4,5,6,7,7,0,1,2,4,4,4]
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
        // 2018/1/30 : 1ms
        if (nums == null || nums.length == 0) return 0;
        int l = 0;
        int r = nums.length - 1;
        while (l < r && nums[l] >= nums[r]) {
            int m = l + (r - l) / 2;
            if (nums[m] < nums[l]) {
                // rotated center in l...m
                r = m;
            } else if (nums[m] == nums[l]) {
                l++;
            } else {
                // nums[m] > nums[l]
                // rotated center in m+1...r
                l = m + 1;
            }
        }
        return nums[l];
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2018_01_30
 *Language: Java
 *
 */

class Solution {
    public int findMin(int[] nums) {
        // 2018/1/30 : 1ms
        if (nums == null || nums.length == 0) return 0;
        int l = 0;
        int r = nums.length - 1;
        while(l<r){
            int m = l + (r - l) / 2;
            if (nums[m] > nums[r]) {
                // center : m+1...r
                l = m + 1;
            } else if (nums[m] == nums[r]) {
                // center not in r
                r--;
            } else {
                // center : l...m
                r = m;
            }
        }
        return nums[l];
    }
}

```


##### *Method #3*
``` java
/*
 *Author: yeh
 *Time: 2018_01_30
 *Language: Java
 *
 */

class Solution {
    public int findMin(int[] nums) {
        // 2018/1/30 : 1ms
        if (nums == null || nums.length == 0) return 0;
        int res = Integer.MAX_VALUE;
        for (int val : nums) {
            res = Math.min(res, val);
        }
        return res;
    }
}

```