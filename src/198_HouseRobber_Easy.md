


### Leetcode 198
#### [House Robber](https://leetcode.com/problems/house-robber)

  

##### ***Problem:***

	You are a professional robber planning to rob houses along a street.
	Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.
	Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.
	
##### ***Example:***

    Input: [1,3,2,1,4]
        Output: 7

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_08
 *Language: Java
 *
 */

class Solution {
    public int rob(int[] nums) {
        // 2018/2/8 : 0ms
        if (nums == null || nums.length == 0) return 0;
        // dp :
        // rob[i] : rob(nums[0, i] + used nums[i])
        // nrob[i] : rob(nums[0, i] - elem used in rob[i])
        // rob[i] = nrob[i - 1] + nums[i]
        // nrob[i] = max(rob[i - 1], nrob[i - 1])
        int rob = 0, nrob = 0;
        for (int i = 0; i < nums.length; i++) {
            int cur = rob; // cur := rob[i - 1]
            rob = nrob + nums[i];
            nrob = Math.max(cur, nrob);
        }
        return Math.max(rob, nrob);
    }
}

```


