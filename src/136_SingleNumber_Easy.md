

### Leetcode 136
#### [Single Number](https://leetcode.com/problems/single-number)

  

##### ***Problem:***

    Given an array of integers, every element appears twice except for one. 
    Find that single one.

    Your algorithm should have a linear runtime complexity. 
    Could you implement it without using extra memory?

    
##### ***Example:***

    Input: [1,2,2]
        Output: 1

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_23
 *Language: Java
 *
 */

class Solution {
    public int singleNumber(int[] nums) {
        int single = 0;
        for (int num : nums) {
            single ^= num;
        }
        return single;
    }
}

```


