


### Leetcode 189
#### [Rotate Array](https://leetcode.com/problems/rotate-array)

  

##### ***Problem:***

	Rotate an array of n elements to the right by k steps.
	
##### ***Example:***

    Input: [1,2,3,4,5,6,7], 3
        Output: [5,6,7,1,2,3,4]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_07
 *Language: Java
 *
 */

class Solution {
    public void rotate(int[] nums, int k) {
        // 2018/2/7 : 1ms
        // reverse two part and then reverse whole
        if (nums == null || nums.length == 0) return;
        k = (k % nums.length + nums.length) % nums.length;
        if (k == 0) return;
        // import org.apache.commons.lang3.ArrayUtils; // not exist in oj
        // use func in ArrayUtils : 
        // public static void reverse(int[] array, int startIndexInclusive, int endIndexExclusive)
        reverse(nums, 0, nums.length - k);
        reverse(nums, nums.length - k, nums.length);
        reverse(nums, 0, nums.length);
    }
    private void reverse(int[] array, int startIndexInclusive, int endIndexExclusive) {
        // reverse nums[s, e)
        endIndexExclusive--;
        while (startIndexInclusive < endIndexExclusive) swap(array, startIndexInclusive++, endIndexExclusive--);
    }
    private void swap(int[] nums, int i, int j) {
        int t = nums[i]; nums[i] = nums[j]; nums[j] = t;
    }
}



```








