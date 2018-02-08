

### Leetcode 66
#### [Plus One](https://leetcode.com/problems/plus-one)

##### ***Problem:***

    Given a non-negative integer 
    represented as a non-empty array of digits, 
    plus one to the integer.

    You may assume the integer do not contain any leading zero, 
    except the number 0 itself.

    The digits are stored such that 
    the most significant digit is at the head of the list.


##### ***Example:***
 
    Input: [0]
    Ouput: [1]
    

##### *Method: #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_05
 *Language: Java
 *
 */

public class Solution {
    public int[] plusOne(int[] digits) {
        if (digits == null) return new int[]{ 1};
        int carry = 0;
        digits[digits.length - 1]++;
        for (int i = digits.length - 1; i >= 0; i--) {
            digits[i] = digits[i] + carry;
            if (digits[i] < 10) return digits;
            carry = 1;
            digits[i] -= 10;
        }
        if (carry > 0) {
            int[] newdigits = new int[digits.length + 1];
            newdigits[0] = carry;
            digits = newdigits;
        }
        return digits;
    }
}

```

