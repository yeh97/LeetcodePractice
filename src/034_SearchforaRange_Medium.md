

### Leetcode 34
#### [Search for a Range](https://leetcode.com/problems/search-for-a-range)

  

##### ***Problem:***

    Given an array of integers sorted in ascending order, 
    find the starting and ending position of a given target value.

    Your algorithm's runtime complexity must be in the order of O(log n).
    
    If the target is not found in the array, return [-1, -1].

    
    
##### ***Example:***

    Input: [5, 7, 7, 8, 8, 10], 8
        Output: [3, 4]
    Input: [5, 7, 7, 8, 8, 10], 9
        Ouput: [-1, -1]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_20
 *Language: Java
 *
 */

public class Solution {
    public int[] searchRange(int[] nums, int target) {
        if (nums==null || nums.length==0) {
            return new int[]{-1, -1};
        }
        int low = binarySearchLow(nums, target, 0, nums.length-1);
        int up = binarySearchUp(nums, target, 0, nums.length-1);
        if (low > up-1) {
            return new int[]{-1, -1};
        } else {
            return new int[]{low, up-1};
        }
    }
    //C++ : lower_bound
    //nums[index] >= target, return the min of index
    private static int binarySearchLow(int[] nums, int target, int start, int end) {
        if (start > end) {
            return start;
        }
        int mid = start + (end - start) / 2;
        if (nums[mid] < target) {
            return binarySearchLow(nums, target, mid+1, end);
        } else {
            return binarySearchLow(nums, target, start, mid-1);
        }
    }
    //C++ : upper_bound
    //nums[index] > target, return the min of index
    private static int binarySearchUp(int[] nums, int target, int start, int end) {
        if (start > end) {
            return start;
        }
        int mid = start + (end - start) / 2;
        if (nums[mid] > target) {
            return binarySearchUp(nums, target, start, mid-1);
        } else {
            return binarySearchUp(nums, target, mid+1, end);
        }
    }
}

```

