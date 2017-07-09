

### Leetcode 8
#### [String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi)
  
    Implement atoi to convert a string to an integer.

**Hint:**

    Carefully consider all possible input cases. 
    If you want a challenge, 
    please do not see below and ask yourself 
    what are the possible input cases.
**Notes:**

    It is intended for this problem to be specified vaguely 
    (ie, no given input specs). 
    You are responsible to gather all the input requirements up front.

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_07
 *Language: Java
 *
 */
public class Solution {
    public static final int intmaxf = Integer.MAX_VALUE/10;
    public static final int intmaxm = Integer.MAX_VALUE%10;
    public int myAtoi(String str) {
        if(str==null) return 0;
        char[] sarray = str.toCharArray();
        int index = 0;
        int val = 0;
        boolean bigThanZero = true;
        //avoid whitespace
        while(index<sarray.length && sarray[index]==' ') index++;
        //sign of the number
        if(index<sarray.length && (sarray[index] == '+' || sarray[index] == '-')) {
            bigThanZero = sarray[index] == '-' ? false : true;
            index++;
        }
        //abs of the number
        while(index<sarray.length && sarray[index]>='0' && sarray[index]<='9') {
            //overflow
            if(val>intmaxf || (val==intmaxf && (int)(sarray[index]-'0')>intmaxm)) {
                return bigThanZero ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            }
            val = val*10 + (int)(sarray[index]-'0');
            index++;
        }
        return bigThanZero ? val : -val;
    }
}
```


