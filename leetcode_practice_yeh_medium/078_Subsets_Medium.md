

### Leetcode 78
#### [Subsets](https://leetcode.com/problems/subsets)

  

##### ***Problem:***

    Given a set of distinct integers, nums, return all possible subsets.

    The solution set must not contain duplicate subsets.


##### ***Example:***

    Input: [1,2]
        Output: [[], [1], [2], [1,2]]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_07
 *Language: Java
 *
 */

public class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        if (nums == null || nums.length == 0) return ret;
        //empty set is subset of any set
        List<Integer> newSubSet = new ArrayList<Integer>();
        ret.add(newSubSet);
        for (int i = 0; i < nums.length; i++) {
            for (int j = ret.size() - 1; j >= 0; j--) {
                newSubSet = new ArrayList<Integer>(ret.get(j));
                newSubSet.add(nums[i]);
                ret.add(newSubSet);
            }
        }
        return ret;
    }
}
```


