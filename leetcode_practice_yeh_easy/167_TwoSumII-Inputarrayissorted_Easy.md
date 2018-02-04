


### Leetcode 167
#### [Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted)

  

##### ***Problem:***

    Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

	The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

	You may assume that each input would have exactly one solution and you may not use the same element twice.
    
##### ***Example:***

    Input: [2,4,6], 6
        Output: [1,2]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_04
 *Language: Java
 *
 */

public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        // 2018/2/4 : 1ms
        // double pointer, sorted array
        // O(N), N = numbers.length
        if (numbers == null || numbers.length < 2) return null;
        int s = 0, e = numbers.length - 1;
        while (e > s) {
            int sum = numbers[s] + numbers[e];
            if (sum > target) e--;
            else if (sum < target) s++;
            else return new int[]{s + 1, e + 1};
        }
        return null;
    }
}


```


