

### Leetcode 53
#### [Maximum Subarray](https://leetcode.com/problems/maximum-subarray)

##### ***Problem:***

    Find the contiguous subarray within an array 
    (containing at least one number) which has the largest sum.


##### ***Example:***
 
    Input: [-2,1,-3,4,-1,2,1,-5,4]
    Ouput: 6 ([4,-1,2,1])
    

##### *Method: #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_01
 *Language: Java
 *
 */

public class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int sum = 0;
        int max = nums[0];
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            max = Math.max(sum, max);
            sum = Math.max(0, sum);
        }
        return max;
    }
}

```

