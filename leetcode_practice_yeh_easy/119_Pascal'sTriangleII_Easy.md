

### Leetcode 119
#### [Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii)

  

##### ***Problem:***

    Given an index k, 
    return the k-th row of the Pascal's triangle.
    

##### ***Example:***

    Input: 0
        Output: [1]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_14
 *Language: Java
 *
 */

public class Solution {
    public List<Integer> getRow(int rowIndex) {
        // C(0, 0) = 1
        // C(n, k) = n! / (n - k)! / k!
        // C(n, k + 1) = C(n, k) * (n - k) / (k + 1)
        List<Integer> ret = new ArrayList<Integer>();
        if (rowIndex < 0) return ret;
        ret.add(1);
        int midup = rowIndex / 2 + 1;
        for (int i = 1; i < midup; i++) {
            // use int would overflow
            long val = (long) (ret.get(i - 1)) * (rowIndex - i + 1) / i;
            ret.add((int) val);
        }
        for (int i = midup; i <= rowIndex; i++) {
            ret.add(ret.get(rowIndex - i));
        }
        return ret;
    }
}

```


