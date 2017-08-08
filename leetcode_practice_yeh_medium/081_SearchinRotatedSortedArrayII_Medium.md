

### Leetcode 81
#### [Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii)

  

##### ***Problem:***

    Follow up for "Search in Rotated Sorted Array":
    What if duplicates are allowed?

    Would this affect the run-time complexity? How and why?

##### ***Example:***

    Input: [1,1,1,2,2,3], 2
        Output: true

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_08
 *Language: Java
 *
 */

public class Solution {
    public boolean search(int[] nums, int target) {
        if(nums == null || nums.length == 0) return false;
        //different from : Search in Rotated Sorted Array
        //nums[left] == nums[mid], can't judge skipping direction
        //run-time complexity : O(lgn) --> O(n)
        int left = 0;
        int right = nums.length-1;
        int mid = (left+right)/2;
        while (left < right){
            if (target == nums[mid]) return true;
            if (nums[left] < nums[mid]) {
                //left sorted
                if (nums[left] <= target && target < nums[mid]) {
                    //in left
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else if (nums[left] > nums[mid]) {
                //right sorted
                if (nums[mid] < target && target <= nums[right]) {
                    //in right
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            } else {
                left++;
            }
            mid = left + (right - left) / 2;
        }
        return nums[mid] == target;
    }
}

```


