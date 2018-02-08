

### Leetcode 67
#### [Add Binary](https://leetcode.com/problems/add-binary)

##### ***Problem:***

    Given two binary strings, return their sum (also a binary string).


##### ***Example:***
 
    Input: "11", "1"
    Ouput: "100"
    

##### *Method: #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_05
 *Language: Java
 *
 */

public class Solution {
    public String addBinary(String a, String b) {
        if (a == null || b == null) {
            if (a == null && b == null) return "0";
            else if (a != null) return new String(a);
            else return new String(b);
        }
        return new String(addBinary(a.toCharArray(), b.toCharArray()));
    }
    private char[] addBinary(char[] a, char[] b) {
        if (a.length < b.length) return addBinary(b, a);
        int carry = 0;
        int aindex = a.length - 1;
        int bindex = b.length - 1;
        while (bindex >= 0) {
            a[aindex] += b[bindex] - '0' + carry;
            if (a[aindex] > '1') {
                carry = 1;
                a[aindex] -= 2;
            } else {
                carry = 0;
            }
            aindex--;
            bindex--;
        }
        if (carry == 1) {
            while (aindex >= 0) {
                a[aindex] += carry;
                if (a[aindex] > '1') {
                    carry = 1;
                    a[aindex] -= 2;
                } else {
                    carry = 0;
                }
                aindex--;
            }
        }
        if (carry == 1) {
            char[] newa = new char[a.length + 1];
            for (int i = 1; i < newa.length; i++) {
                newa[i] = a[i - 1];
            }
            newa[0] = '1';
            a = newa;
        }
        return a;
    }
}

```

