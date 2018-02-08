

### Leetcode 55
#### [Jump Game](https://leetcode.com/problems/jump-game)

  

##### ***Problem:***

    Given an array of non-negative integers, 
    you are initially positioned at the first index of the array.

    Each element in the array represents your maximum jump length at that position.
    
##### ***Note:***

    1) not necessary jump out the array
    
##### ***Example:***

    Input: [0, 1]
        Output: false


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_02
 *Language: Java
 *
 */

public class Solution {
    public boolean canJump(int[] nums) {
        if (nums == null || nums.length < 2) {
            return true;
        }
        //assert (nums[i] > 0)
        //(nums[i] + i) is max index in next jump
        int maxJump = nums[0] + 0;
        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] == 0) {
                if (maxJump <= i) return false;
            } else {
                maxJump = Math.max(maxJump, nums[i] + i);
            }
        }
        return true;
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_02
 *Language: Java
 *
 */

public class Solution {
    public boolean canJump(int[] nums) {
        if (nums == null || nums.length < 2) return true;
        int canArrive = nums.length - 1;
        for (int i = nums.length - 2; i >= 0; i--) {
            if (nums[i] + i < canArrive) continue;
            //from i, can jump to canArrive
            canArrive = i;
        }
        //canArrive == 0, 
        //means that can arrive nums.length-1 from 0
        return canArrive == 0;
    }
}

```

