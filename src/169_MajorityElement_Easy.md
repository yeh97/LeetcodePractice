


### Leetcode 169
#### [Majority Element](https://leetcode.com/problems/majority-element)

  

##### ***Problem:***

    Given an array of size n, find the majority element. 
    The majority element is the element that appears more than ⌊ n/2 ⌋ times.
    You may assume that the array is non-empty and the majority element always exist in the array.
    
##### ***Example:***

    Input: [2,1,2]
        Output: 2


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_04
 *Language: Java
 *
 */

public class Solution {
    public int majorityElement(int[] nums) {
        // 2018/2/4 : 2ms
        if (nums == null || nums.length == 0) return 0; // err
        // https://gregable.com/2013/10/majority-vote-algorithm-find-majority.html
        // Majority Voting Algorithm - Find the majority element in a list of values
        int candidate = 0, count = 0;
        for (int val : nums) {
            if (count == 0) candidate = val;
            if (candidate == val) count++;
            else count--;
        }
        return candidate;
    }
}

```


