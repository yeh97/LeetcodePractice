

### Leetcode 39
#### [Combination Sum](https://leetcode.com/problems/combination-sum)

  

##### ***Problem:***

    Given a set of candidate numbers (C) (without duplicates) and a target number (T), 
    find all unique combinations in C where the candidate numbers sums to T.

    The same repeated number may be chosen from C unlimited number of times.

##### ***Note:***
    1) All numbers (including target) will be positive integers.
    2) The solution set must not contain duplicate combinations.
    
    
##### ***Example:***

    Input: [2, 3, 6, 7], 7
        Output: [ [7], [2, 2, 3] ]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_29
 *Language: Java
 *
 */

public class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ret = new LinkedList<List<Integer>>();
        if (candidates == null || target <= 0) return ret;
        Arrays.sort(candidates);
        List<Integer> combination = new LinkedList<Integer>();
        combinationSumDfs(ret, combination, candidates, 0, target);
        return ret;
    }
    private void combinationSumDfs(List<List<Integer>> list, List<Integer> combination,
                                   int[] candidates, int s, int t) {
        if (t == 0) {
            List<Integer> solution = new LinkedList<Integer>();
            solution.addAll(combination);
            list.add(solution);
        } else if (t > 0) {
            for (int i = s; i < candidates.length; i++) {
                combination.add(candidates[i]);
                combinationSumDfs(list, combination, candidates, i, t-candidates[i]);
                combination.remove(combination.size() - 1);
            }
        }
    }
}

```

