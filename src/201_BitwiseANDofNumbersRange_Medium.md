


### Leetcode 201
#### [Bitwise AND of Numbers Range](https://leetcode.com/problems/bitwise-and-of-numbers-range)

  

##### ***Problem:***

	Given a range [m, n] where 0 <= m <= n <= 2147483647, 
	return the bitwise AND of all numbers in this range, inclusive.
	
##### ***Example:***

    Input: 5,7
        Output: 4 (5&6&7)

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_09
 *Language: Java
 *
 */

class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        // 2018/2/9 : 11ms
        if (m < 0 || n < 0 || m > n) return 0;
        // find same bit-left between n and m, let bit-right is '0'
        int i = 0;
        while (m != n) {
            m >>= 1;
            n >>= 1;
            i++;
        }
        return n << i;
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2018_02_09
 *Language: Java
 *
 */

class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        // 2018/2/9 : 11ms
        if (m < 0 || n < 0 || m > n) return 0;
        // find same bit-left between n and m, let bit-right is '0'
        // n = n & (n - 1), --> delete rightest bit '1'
        // if m >= n, --> diff bit-right is '0'
        while (m < n) n &= (n - 1);
        return n;
    }
}


```

