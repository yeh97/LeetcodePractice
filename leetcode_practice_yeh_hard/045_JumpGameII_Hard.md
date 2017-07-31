

### Leetcode 45
#### [Jump Game II](https://leetcode.com/problems/jump-game-ii)

  

##### ***Problem:***

    Given an array of non-negative integers, 
    you are initially positioned at the first index of the array.

    Each element in the array represents your maximum jump length at that position.

    Your goal is to reach the last index in the minimum number of jumps.
    
    
##### ***Example:***

    Input: [2,3,1,1,4]
        Output: 2
    Input: [2]
        Output: 0

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_31
 *Language: Java
 *
 */

public class Solution {
    public int jump(int[] nums) {
        if (nums == null || nums.length < 2) {
            return 0;
        }
        //assert (nums[i] > 0)
        //(nums[i] + i) is max index in next jump
        int ret = 0;
        int l = 0;
        int start = 0;
        int nextJump;
        while (start < nums.length) {
            ret++;
            if (nums[start] + start >= nums.length - 1) {
                //final jump
                break;
            } else {
                nextJump = maxJumpIndex(nums, l + 1, start + nums[start] + 1);
                l = start + nums[start];
                start = nextJump;
            }
        }
        return ret;
    }
    private int maxJumpIndex(int[] nums, int s, int e) {
        int ret = s;
        int maxLength = nums[s] + s;
        for (int i = s + 1; i < e; i++) {
            if (nums[i] + i > maxLength) {
                ret = i;
                maxLength = nums[i] + i;
            }
        }
        return ret;
    }
}

```


