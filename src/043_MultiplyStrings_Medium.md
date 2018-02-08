

### Leetcode 43
#### [Multiply Strings](https://leetcode.com/problems/multiply-strings)

  

##### ***Problem:***

    Given two non-negative integers num1 and num2 represented as strings, 
    return the product of num1 and num2.

##### ***Note:***
    1) The length of both num1 and num2 is < 110.
    2) Both num1 and num2 contains only digits 0-9.
    3) Both num1 and num2 does not contain any leading zero.
    
    
##### ***Example:***

    Input: "0", "0"
        Output: "0"
    Input: "7", "9"
        Output: "63"


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_29
 *Language: Java
 *
 */

public class Solution {
    public String multiply(String num1, String num2) {
        if (num1==null || num2==null) return "0";
        if (num1.length()==0 || num2.length()==0) return "0";
        if (num1.length() > num2.length()) return multiply(num2, num1);
        int[] n1 = toIntArray(num1);
        int[] n2 = toIntArray(num2);
        int[] ret = new int[n1.length + n2.length];
        int carry = 0;
        int current = 0;
        for (int i = n1.length - 1; i >= 0; i--) {
            for (int j = n2.length - 1; j >= 0; j--) {
                current = n1[i] * n2[j] + carry + ret[i + j + 1];
                ret[i + j + 1] = current % 10;
                carry = current / 10;
            }
            current = carry + ret[i];
            ret[i] = current % 10;
            carry = current / 10;
        }
        int start = firstNoZero(ret);
        if (start == -1) {
            return "0";
        } else {
            return toString(ret, start, ret.length);
        }
    }
    //convert num to Integer Array
    private int[] toIntArray(String num) {
        //assert(num != null)
        //num is made of '0'...'9', has no lead-zeros
        int[] ret = new int[num.length()];
        for (int i = num.length() - 1; i >= 0; i--) {
            ret[i] = (int) (num.charAt(i) - '0');
        }
        return ret;
    }
    //convert num[s,e) to String
    private String toString(int[] num, int s, int e) {
        //assert(num != null)
        //0 <= num[i] <= 9
        char[] ret = new char[e - s];
        for (int i = s; i < e; i++) {
            ret[i - s] = (char) (num[i] + '0');
        }
        return new String(ret);
    }
    //num[i] != 0, return min of i
    //if i not exist, return -1
    private int firstNoZero(int[] num) {
        for (int i = 0; i < num.length; i++) {
            if (num[i] != 0) return i;
        }
        return -1;
    }
}

```

