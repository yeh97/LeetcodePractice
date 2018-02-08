

### Leetcode 50
#### [Pow(x, n)](https://leetcode.com/problems/powx-n)

  

##### ***Problem:***

    Implement pow(x, n).
    
##### ***Note:***

    1) n == Integer.MIN_VALUE
    
##### ***Example:***

    Input: 1.1, 2
        Output: 1.21


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_31
 *Language: Java
 *
 */

public class Solution {
    public double myPow(double x, int n) {
        //quick pow
        //attention : n == Integer.MIN_VALUE
        if (n < 0) return 1.0/myPow(x, -(n+1))/x;
        double ret = 1.0;
        while (n != 0) {
            if (n%2 == 1) {
                ret *= x;
            }
            x *= x;
            n >>= 1;
        }
        return ret;
    }
}

```

