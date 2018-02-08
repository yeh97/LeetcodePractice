

### Leetcode 90
#### [Subsets II](https://leetcode.com/problems/subsets-ii)

  

##### ***Problem:***

    Given a collection of integers that might contain duplicates, nums, return all possible subsets.

    Note: The solution set must not contain duplicate subsets.

##### ***Example:***

    Input: [1,1]
        Output: [[], [1], [1, 1]]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_09
 *Language: Java
 *
 */

public class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        List<Integer> subset = new ArrayList<Integer>();
        ret.add(subset);
        //empty set
        if (nums == null || nums.length == 0) return ret;
        Arrays.sort(nums);
        int pre = -1;
        int end = -1;
        for (int i = 0; i < nums.length; i++) {
            end = (i > 0 && nums[i] == nums[i - 1]) ? pre : -1;
            pre = ret.size() - 1;
            for (int j = pre; j > end; j--) {
                subset = new ArrayList(ret.get(j));
                subset.add(nums[i]);
                ret.add(subset);
            }
        }
        return ret;
    }
}
```


