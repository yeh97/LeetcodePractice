

### Leetcode 137
#### [Single Number II](https://leetcode.com/problems/single-number-ii)

  

##### ***Problem:***

    Given an array of integers, 
    every element appears three times except for one, 
    which appears exactly once. Find that single one.

    Your algorithm should have a linear runtime complexity. 
    Could you implement it without using extra memory?

    
##### ***Example:***

    Input: [1,2,2,2]
        Output: 1

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_23
 *Language: Java
 *
 */

public class Solution {
    public int singleNumber(int[] nums) {
        // (0, 0) -> (0, 1) -> (1, 1) -> (0, 0)
        // a = a ^ b, b = b ^ ~a
        // --> b : 0 -> 1 -> 1 -> 0
        int a = 0;
        int b = 0;
        int x, y, c, d;
        for (int num : nums) {
            x = a & num;
            y = b & num;
            c = num & (x ^ y);
            d = num & (y ^ ~c);
            a = (a ^ x) | c;
            b = (b ^ y) | d;
        }
        return b;
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_23
 *Language: Java
 *
 */

public class Solution {
    public int singleNumber(int[] nums) {
        // a : ones
        // b : twos
        int a = 0;
        int b = 0;
        for (int num : nums) {
            a = (a ^ num) & ~b;
            b = (b ^ num) & ~a;
        }
        return a;
    }
}


```


