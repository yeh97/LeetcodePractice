


### Leetcode 199
#### [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view)

  

##### ***Problem:***

	Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.
	
##### ***Example:***

    Input: [1,2,3,4,5]
        Output: [1,3,5]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_08
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
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        // 2018/2/8 : 2ms
        List<Integer> res = new ArrayList<Integer>();
        if (root == null) return res;
        Deque<TreeNode> deq = new LinkedList<TreeNode>();
        deq.offer(root);
        while (deq.size() > 0) {
            // the rightest elem in this hight
            res.add(deq.getLast().val);
            // add elem with same hight
            for (int i = deq.size(); i > 0; i--) {
                TreeNode cur = deq.remove();
                if (cur.left != null) deq.offer(cur.left);
                if (cur.right != null) deq.offer(cur.right);
            }
        }
        return res;
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2018_02_08
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
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        // 2018/2/8 : 1ms
        List<Integer> res = new ArrayList<Integer>();
        DFS(root, res, 1);
        return res;
    }
    private void DFS(TreeNode root, List<Integer> list, int hight) {
        if (root == null) return;
        // explored-depth == list.size()
        if (hight > list.size()) list.add(root.val);
        DFS(root.right, list, hight + 1);
        DFS(root.left, list, hight + 1);
    }
}

```





