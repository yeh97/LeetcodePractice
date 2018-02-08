

### Leetcode 27
#### [Remove Element](https://leetcode.com/problems/remove-element)

##### ***Problem:***

    Given an array and a value, 
    remove all instances of that value 
    in place and return the new length.

    Do not allocate extra space for another array, 
    you must do this in place with constant memory.

    The order of elements can be changed.
    It doesn't matter what you leave beyond the new length.


##### ***Example:***
 
    Input: [3,2,2,3], 3
    Ouput: 2 ([2,2])
    

  
##### *Method: #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_12
 *Language: Java
 *
 */

public class Solution {
    public int removeElement(int[] nums, int val) {
        if(nums==null || nums.length==0) return 0;
        int size = 0;
        for(int i=0; i<nums.length; i++) {
            if(nums[i] != val) {
                nums[size++] = nums[i];
            }
        }
        return size;
    }
}

```
