

### Leetcode 46
#### [Permutations](https://leetcode.com/problems/permutations)

  

##### ***Problem:***

    Given a collection of distinct numbers, return all possible permutations.

##### ***Note:***
    1) distinct numbers
    
    
##### ***Example:***

    Input: [1,2]
        Output: [ [1,2], [2,1] ]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_31
 *Language: Java
 *
 */

public class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ret = new LinkedList<List<Integer>>();
        if (nums == null || nums.length == 0) {
            return ret;
        } else {
            //O(n^^n) times
            permuteDFS(nums, new boolean[nums.length], 0, ret, new int[nums.length]);
            return ret;
        }
    }
    private void permuteDFS(int[] nums, boolean[] used, int step, 
                       List<List<Integer>> list, int[] permutation) {
        if (step >= nums.length) {
            List<Integer> solution = new LinkedList<Integer>();
            for (int i = 0; i < nums.length; i++) {
                solution.add(permutation[i]);
            }
            list.add(solution);
        } else {
            for (int i = 0; i < nums.length; i++) {
                if (used[i]) continue;
                used[i] = true;
                permutation[step] = nums[i];
                permuteDFS(nums, used, step+1, list, permutation);
                used[i] = false;
            }
        }
    }
}

```

