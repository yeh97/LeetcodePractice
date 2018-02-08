

### Leetcode 60
#### [Permutation Sequence](https://leetcode.com/problems/permutation-sequence)

  

##### ***Problem:***

    The set [1,2,3,…,n] contains a total of n! unique permutations.
    Given n and k, return the k-th permutation sequence according to alphabet order.
    
##### ***Note:***

    1) Given n will be between 1 and 9 inclusive
    
##### ***Example:***

    Input: 2, 1
        Output: "12"


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_03
 *Language: Java
 *
 */

public class Solution {
    //n! : 0...9
    private static final int factorial[] = {1, 1, 2, 6, 24, 120, 720, 5040, 40320, 362880};
    public String getPermutation(int n, int k) {
        //Given n will be between 1 and 9 inclusive
        if (n < 1 || n > 9 || k < 0) return null;
        StringBuilder ret = new StringBuilder();
        k = (k - 1) % factorial[n];
        boolean[] used = new boolean[n];
        for (int i = n - 1; i >= 0; i--) {
            //new element added to string
            int val = getUnusedIndex(used, k / factorial[i] + 1);
            ret.append(val + 1);
            used[val] = true;
            k %= factorial[i];
        }
        return ret.toString();
    }
    //return index of K-th unused element
    private int getUnusedIndex(boolean[] used, int k) {
        if (used == null || k <= 0) return -1;
        for (int i = 0; i < used.length; i++) {
            if (used[i]) continue;
            else k--;
            if (k == 0) return i;
        }
        return -1;
    }
}

```

