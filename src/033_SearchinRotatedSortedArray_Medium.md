

### Leetcode 33
#### [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array)

  

##### ***Problem:***

    Suppose an array sorted in ascending order
    is rotated at some pivot unknown to you beforehand.

    (i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

    You are given a target value to search. 
    
    If found in the array return its index, otherwise return -1.

    You may assume no duplicate exists in the array.
    
##### ***Example:***

    Input: [4,5,6,7,0,1,2], 0
        Output: 4
    Input: [4,5,6,7,0,1,2], 8
        Ouput: -1

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_16
 *Language: Java
 *
 */

public class Solution {
    public int search(int[] nums, int target) {
        if(nums==null || nums.length==0) return -1;
        //every i in 1...n,
        //A: nums[1]...nums[i], 
        //B: nums[i+1]...nums[n],
        //if sorted nums rotated at a position, 
        //(A is sorted || B is sorted) == true
        int left = 0;
        int right = nums.length-1;
        int mid = (left+right)/2;
        while(left < right){
            if(target == nums[mid]) return mid;
            if(nums[left] <= nums[mid]) {
                //left sorted
                if(nums[left]<=target && target<nums[mid]) {
                    //in left
                    right = mid - 1;
                }else{
                    left = mid + 1;
                }
            }else{
                //right sorted
                if(nums[mid]<target && target<=nums[right]) {
                    //in right
                    left = mid + 1;
                }else{
                    right = mid - 1;
                }
            }
            mid = (right+left)/2;
        }
        return (nums[mid]==target) ? mid:-1;
    }
}

```

