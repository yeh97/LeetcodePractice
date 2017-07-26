

### Leetcode 35
#### [Search Insert Position](https://leetcode.com/problems/search-insert-position)

##### ***Problem:***

    Given a sorted array and a target value, 
    return the index if the target is found. 
    
    If not, return the index where it would be if it were inserted in order.
    
    You may assume no duplicates in the array.


##### ***Example:***
 
    Input: [1,3,5,6], 5
    Ouput: 2
    

##### *Method: #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_26
 *Language: Java
 *
 */

public class Solution {
    public int searchInsert(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        return binarySearchLow(nums, target, 0, nums.length - 1);
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
}

```

