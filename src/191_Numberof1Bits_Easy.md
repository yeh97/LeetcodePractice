


### Leetcode 191
#### [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits)

  

##### ***Problem:***

	returns the number of ’1' bits of a given 32 bits unsigned integer.
	
##### ***Example:***

    Input: 43261596 (00000010100101000001111010011100)
        Output: 12

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_07
 *Language: Java
 *
 */

public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        // 2018/2/7 : 2ms
        return n == 0 ? 0 : ((n & 1) + hammingWeight(n >>> 1));
    }
}

```








