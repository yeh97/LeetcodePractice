

### Leetcode 40
#### [Combination Sum II](https://leetcode.com/problems/combination-sum-ii)

  

##### ***Problem:***

    Given a set of candidate numbers (C) (without duplicates) and a target number (T), 
    find all unique combinations in C where the candidate numbers sums to T.

    Each number in C may only be used once in the combination.

##### ***Note:***
    1) All numbers (including target) will be positive integers.
    2) The solution set must not contain duplicate combinations.
    
    
##### ***Example:***

    Input: [10, 1, 2, 7, 6, 1, 5], 8
        Output: [ [1, 7], [1, 2, 5],
                [2, 6], [1, 1, 6] ]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_29
 *Language: Java
 *
 */

public class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> ret = new LinkedList<List<Integer>>();
        if (candidates == null || target <= 0) return ret;
        Arrays.sort(candidates);
        List<Integer> combination = new LinkedList<Integer>();
        combinationSum2Dfs(ret, combination, candidates, 0, target);
        return ret;
    }
    private void combinationSum2Dfs(List<List<Integer>> list, List<Integer> combination,
                                   int[] candidates, int s, int t) {
        if (t == 0) {
            List<Integer> solution = new LinkedList<Integer>();
            solution.addAll(combination);
            list.add(solution);
        } else if (t > 0) {
            for (int i = s; i < candidates.length; i++) {
                if (i > s && candidates[i] == candidates[i-1]) continue;
                combination.add(candidates[i]);
                combinationSum2Dfs(list, combination, candidates, i+1, t-candidates[i]);
                combination.remove(combination.size() - 1);
            }
        }
    }
}


```

