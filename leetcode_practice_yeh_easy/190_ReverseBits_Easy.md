


### Leetcode 190
#### [Reverse Bits](https://leetcode.com/problems/reverse-bits)

  

##### ***Problem:***

	Reverse bits of a given 32 bits unsigned integer.
	
##### ***Example:***

    Input: 43261596 (00000010100101000001111010011100)
        Output: 964176192 (00111001011110000010100101000000)


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_07
 *Language: Java
 *
 */

public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        // 2018/2/7 : 2ms
        int res = 0;
        // Integer : 32-bit
        for (int i = 0; i < 32; i++) {
            res = (res << 1) | (n & 1);
            n >>>= 1; // unsiged right-move
        }
        return res;
    }
}

```








