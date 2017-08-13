

### Leetcode 113
#### [Path Sum II](https://leetcode.com/problems/path-sum-ii)

  

##### ***Problem:***

    Given a binary tree and a sum,
    find all root-to-leaf paths 
    where each path's sum equals the given sum.


##### ***Example:***

    Input: [1,2], 3
        Output: [[1,2]]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_13
 *Language: Java
 *
 */

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> ret = new LinkedList<List<Integer>>();
        List<Integer> curPath = new ArrayList<Integer>();
        pathSum(ret, curPath, root, sum);
        return ret;
    }
    private void pathSum(List<List<Integer>> list, List<Integer> path,
                         TreeNode root, int target) {
        if (root == null) return;
        path.add(root.val);
        target -= root.val;
        // if root is a leaf
        if (root.left == null && root.right == null) {
            if (target == 0) list.add(new ArrayList<Integer>(path));
        } else {
            pathSum(list, path, root.left, target);
            pathSum(list, path, root.right, target);
        }
        path.remove(path.size() - 1);
    }
}
```


