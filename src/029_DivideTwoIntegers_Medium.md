

### Leetcode 29
#### [Divide Two Integers](https://leetcode.com/problems/divide-two-integers)

    Divide two integers without using multiplication, 
    division and mod operator.

    If it is overflow, return MAX_INT.
    
***Example:***

    Input: -2147483648, 1
        Ouput: -2147483648(INT_MIN)
    Input: -2147483648, -1
        Ouput: 2147483647(INT_MAX)

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_14
 *Language: Java
 *
 */

public class Solution {
    //dividend / divisor
    public int divide(int dividend, int divisor) {
        //overflow #1: divisor==0
        if(divisor == 0) return Integer.MAX_VALUE;
        //overflow #2: dividend==INT_MIN && divisor==-1, abs(INT_MIN)>INT_MAX
        if(dividend==Integer.MIN_VALUE && divisor==-1) return Integer.MAX_VALUE;
        //get sign of ret : if end, sor has same sign, sign = true
        boolean sign = !((divisor<0) ^ (dividend<0));
        //NOTE: (int)abs(INT_MIN) == INT_MIN
        long end = Math.abs((long)dividend);
        long sor = Math.abs((long)divisor);
        long sortemp;
        long time;
        int ret = 0;
        while(end >= sor) {
            sortemp = sor;
            time = 1;
            while(end >= (sortemp<<1)) {
                sortemp <<= 1;
                time <<= 1;
            }
            ret += time;
            end -= sortemp;
        }
        return sign ? ret:-ret;
    }
}

```
