

### Leetcode 26
#### [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array)

##### ***Problem:***

    Given a sorted array, 
    remove the duplicates in place 
    such that each element appear only once
    and return the new length.

    Do not allocate extra space for another array, 
    you must do this in place with constant memory.


##### ***Example:***
 
    Input: [1,1,2]
    Ouput: 2 
        (with the first two elements of nums being 1 and 2 respectively)
    

  
##### *Method: #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_12
 *Language: Java
 *
 */

public class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums==null || nums.length==0) return 0;
        //the new array's max index
        int end = 0;
        for(int i=1; i<nums.length; i++) {
            if(nums[end] != nums[i]) {
                nums[++end] = nums[i];
            }
        }
        return end+1;
    }
}

```
