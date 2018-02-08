

### Leetcode 77
#### [Combinations](https://leetcode.com/problems/combinations)

  

##### ***Problem:***

    Given two integers n and k, 
    return all possible combinations of k numbers out of 1 ... n.


##### ***Example:***

    Input: 3, 2
        Output: [[1,2], [2,3], [1,3]]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_07
 *Language: Java
 *
 */

public class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> ret = new LinkedList<List<Integer>>();
        if (n <= 0 || k<= 0 || n < k) return ret;
        combineDFS(n, k, -1, ret, new ArrayList<Integer>());
        return ret;
    }
    private void combineDFS(int canUsed, int needUsed, int minUsed,
                           List<List<Integer>> list, List<Integer> solution) {
        if (needUsed == 0) {
            list.add(new LinkedList(solution));
        } else {
            for (int i = minUsed + 1; i <= canUsed - needUsed; i++) {
                solution.add(i + 1);
                combineDFS(canUsed, needUsed - 1, i, list, solution);
                solution.remove(solution.size() - 1);
            }
        }
    }
}

```


