


### Leetcode 222
#### [Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes)


##### ***Problem:***

    Given a complete binary tree, count the number of nodes.

##### ***Example:***

    Input: [1,2,3,4,5,6]
        Output: 6

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_07
 *Language: Python3
 *
 */

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def countNodes(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        def leftHeight(rootl):
            return 1 + leftHeight(rootl.left) if rootl else 0
        if not root:
            return 0
        lh, rh = leftHeight(root.left), leftHeight(root.right)
        if lh == rh:
            return pow(2, lh) + self.countNodes(root.right)
        else:
            return pow(2, rh) + self.countNodes(root.left)

```

