

### Leetcode 70
#### [Climbing Stairs](https://leetcode.com/problems/climbing-stairs)

##### ***Problem:***

    You are climbing a stair case. It takes n steps to reach to the top.

    Each time you can either climb 1 or 2 steps. 
    
    In how many distinct ways can you climb to the top?


##### ***Example:***
 
    Input: 1
        Ouput: 1
    

##### *Method: #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_06
 *Language: Java
 *
 */

public class Solution {
    public int climbStairs(int n) {
        //a[n] = a[n-1] + a[n-2]
        //can use matrix quickpow to O(lgn)
        //O(n)
        if (n < 0) return 0;//illeagle
        int a = 0;
        int b = 1;
        for (int i = 0; i < n; i++) {
            b = a + b;
            a = b - a;
        }
        return b;
    }
}
```

