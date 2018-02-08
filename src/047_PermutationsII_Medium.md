

### Leetcode 47
#### [Permutations II](https://leetcode.com/problems/permutations-ii)

  

##### ***Problem:***

    Given a collection of numbers that might contain duplicates, return all possible unique permutations.

##### ***Note:***
    1) might contain duplicates
    
    
##### ***Example:***

    Input: [1,1,2]
        Output: [ [1,1,2], [2,1,1], [1,2,1] ]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_31
 *Language: Java
 *
 */

public class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> ret = new LinkedList<List<Integer>>();
        if (nums == null || nums.length == 0) {
            return ret;
        } else {
            Arrays.sort(nums);
            permuteUniqueDFS(nums, new boolean[nums.length], 0, ret, new int[nums.length]);
            return ret;
        }
    }
    private void permuteUniqueDFS(int[] nums, boolean[] used, int step,
                                 List<List<Integer>> list, int[] permutation) {
        if (step >= nums.length) {
            List<Integer> solution = new LinkedList<Integer>();
            for (int i = 0; i < nums.length; i++) {
                solution.add(permutation[i]);
            }
            list.add(solution);
        } else {
            for (int i = 0; i < nums.length; i++) {
                //if nums[i]==nums[j], i > j
                //nums[i]->permutation[m], nums[j]->permutation[n]
                //--> m > n
                if (i > 0 && !used[i - 1] && nums[i] == nums[i - 1]) continue;
                if (used[i]) continue;
                used[i] = true;
                permutation[step] = nums[i];
                permuteUniqueDFS(nums, used, step+1, list, permutation);
                used[i] = false;
            }
        }
    }
}

```

