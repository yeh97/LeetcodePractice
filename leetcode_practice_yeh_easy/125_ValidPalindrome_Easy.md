

### Leetcode 125
#### [Valid Palindrome](https://leetcode.com/problems/valid-palindrome)

  

##### ***Problem:***

    Given a string, 
    determine if it is a palindrome,
    considering only alphanumeric characters and ignoring cases.


##### ***Example:***

    Input: "A man, a plan, a canal: Panama"
        Output: true

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_17
 *Language: Java
 *
 */

public class Solution {
    public boolean isPalindrome(String s) {
        if (s == null || s.length() == 0) return true;
        int l = 0;
        int r = s.length() - 1;
        char chl, chr;
        while (l < r) {
            chl = s.charAt(l);
            chr = s.charAt(r);
            if (!isValidChar(chl)) {
                l++;
            } else if (!isValidChar(chr)) {
                r--;
            } else {
                if (!equalChar(chl, chr)) return false;
                l++;
                r--;
            }
        }
        return true;
    }
    private boolean isValidChar(char ch) {
        return Character.isLetter(ch) || Character.isDigit(ch);
    }
    private boolean equalChar(char a, char b) {
        // assert isValidChar(a) && isValidChar(b)
        return Character.toLowerCase(a) == Character.toLowerCase(b);
    }
}

```


