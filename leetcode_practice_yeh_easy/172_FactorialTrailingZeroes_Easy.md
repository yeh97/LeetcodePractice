


### Leetcode 172
#### [Factorial Trailing Zeroes](https://leetcode.com/problems/factorial-trailing-zeroes)

  

##### ***Problem:***

    Given an integer n, return the number of trailing zeroes in n!
    
##### ***Example:***

    Input: 5
        Output: 1


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_04
 *Language: Java
 *
 */

class Solution {
    public int trailingZeroes(int n) {
        // 2018/2/4 : 1ms
        // n! = (2^p) * (5^k)..., p > k
        // num of trailing zeroes = min(p, k) = k
        return n > 0 ? n / 5 + trailingZeroes(n / 5) : 0;
    }
}



```


