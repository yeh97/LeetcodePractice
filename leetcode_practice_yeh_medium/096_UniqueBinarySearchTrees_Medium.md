

### Leetcode 96
#### [Unique Binary Search Trees](https://leetcode.com/problems/binary-tree-inorder-traversal)

  

##### ***Problem:***

    Given n, 
    how many structurally unique BST's (binary search trees) that store values 1...n?
    

##### ***Example:***

    Input: 14
        Output: 2674440

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_10
 *Language: Java
 *
 */

public class Solution {
    public int numTrees(int n) {
        // Catalan[n] = C(2n, n) - C(2n, n - 1)
        // == (2n)! / (n)! / (n + 1)!
        // <--> 
        // Catalan[n + 1] = 2(2n + 1) / (n + 2) * Catalan[n]
        if (n < 1) return 0;
        long ret = 1; // Catalan[1];
        for (int i = 1; i < n; i++) {
            ret = 2 * (2 * i + 1) * ret / (i + 2);
        }
        return (int) ret;
    }
}

```


