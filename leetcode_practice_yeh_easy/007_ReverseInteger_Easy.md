

### Leetcode 7
###### [Reverse Integer](https://leetcode.com/problems/reverse-integer)
  
    Reverse digits of an integer.

**Example1:**

    x = 123, return 321
**Example2:**

    x = -123, return -321
**Note:**

    The input is assumed to be a 32-bit signed integer. 
    Your function should return 0 when the reversed integer overflows

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_07
 *Language: Java
 *
 */
public class Solution {
    public int reverse(int x) {
        // -Integer.MIN_VALUE == Integer.MIN_VALUE
        if(x == Integer.MIN_VALUE) return 0;
        if(x < 0) return -reverse(-x);
        long t = x;
        long ans = 0;
        while(t!=0){
            ans = ans*10 + t%10;
            t /= 10;
        }
        return (ans > Integer.MAX_VALUE) ? 0 : (int)ans;
    }
}

```

