

### Leetcode 65
#### [Valid Number](https://leetcode.com/problems/valid-number)

  

##### ***Problem:***

    Validate if a given string is numeric.
    
##### ***Note:***

    1) may contains space
    2) "1.", ".1" is valid
    3) may contains other char like '(', '&'
##### ***Example:***

    Input: " -1.1e-0   "
        Output: true

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_05
 *Language: Java
 *
 */

public class Solution {
    //valis kinds:
    //1) (space) + float + (space)
    //2) (space) + float + e + integer + (space)
    
    public boolean isNumber(String s) {
        if (s == null) return false;
        s = s.trim();
        if (s.isEmpty()) return false;
        int cutPosition = -1;
        char currentChar;
        for (int i = s.length() - 1; i >= 0; i--) {
            currentChar = s.charAt(i);
            if (currentChar == 'e' || currentChar == 'E') {
                if (cutPosition < 0) cutPosition = i;
                else return false;
            }
        }
        if (cutPosition < 0) {
            return isFloat(s);
        } else if (cutPosition == 0 || cutPosition == s.length() - 1) {
            return false;
        } else {
            return isFloat(s.substring(0, cutPosition)) 
                && isInteger(s.substring(cutPosition + 1, s.length()));
        }
    }
    private int kindOfChar(char ch) {
        if (ch == '+' || ch == '-') return 0;
        if (ch == '.') return 1;
        if (Character.isDigit(ch)) return 2;
        return 3;
    }
    private boolean isInteger(String s) {
        //if (s == null) return false;
        //s = s.trim();
        if (s.isEmpty()) return false;
        int size = s.length();
        boolean hasSignChar = false;
        if (kindOfChar(s.charAt(0)) == 0) hasSignChar = true;
        boolean hasDigit = false;
        int currentCharKind;
        for (int i = hasSignChar ? 1 : 0; i < size; i++) {
            currentCharKind = kindOfChar(s.charAt(i));
            if (currentCharKind == 0) return false;
            else if (currentCharKind == 3) return false;
            else if (currentCharKind == 1) return false;
            else if (currentCharKind == 2) hasDigit = true;
        }
        return hasDigit;
    }
    private boolean isFloat(String s) {
        //if (s == null) return false;
        //s = s.trim();
        if (s.isEmpty()) return false;
        int size = s.length();
        boolean hasSignChar = false;
        if (kindOfChar(s.charAt(0)) == 0) hasSignChar = true;
        //can exist a dot in any position
        boolean hasDot = false;
        boolean hasDigit = false;
        int currentCharKind;
        for (int i = hasSignChar ? 1 : 0; i < size; i++) {
            currentCharKind = kindOfChar(s.charAt(i));
            if (currentCharKind == 0) return false;
            else if (currentCharKind == 3) return false;
            else if (currentCharKind == 2) hasDigit = true;
            else if (currentCharKind == 1) {
                if (hasDot) return false;
                hasDot = true;
            }
        }
        return hasDigit;
    }
}
```
##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_05
 *Language: Java
 *
 */

public class Solution {
    //valis kinds:
    //1) (space) + float + (space)
    //2) (space) + float + e + integer + (space)
    //note : ".1", "3." is valid float
    //input char kinds:
    //1) space; 2) dot; 3) sign; 
    //4) digit; 5) e; 6) unexcepted
    private static int kindOfChar(char ch) {
        if (Character.isSpace(ch)) return 0;
        else if (ch == '.') return 1;
        else if (ch == '+' || ch == '-') return 2;
        else if (Character.isDigit(ch)) return 3;
        else if (ch == 'e' || ch == 'E') return 4;
        else return 5;
    }
    //status:
    //-1) not valid number
    //float status:
    //1) (space)
    //2) (space) + sign
    //3) (space) + (sign) + dot
    //4) (space) + (sign) + digit
    //5) (space) + (sign) + digit + dot
    //|| (space) + (sign) + dot + digit
    //contain 'e':
    //6) float + e
    //7) float + e + sign
    //8) float + e + (sign) + digit
    //end with space:
    //9) validnumber + space
    private static final int[][] trans = {
        //col : input kinds : 1...6
        //row : current status
        {  0,  2,  1,  3, -1, -1},
        { -1,  2, -1,  3, -1, -1},
        { -1, -1, -1,  4, -1, -1},
        {  8,  4, -1,  3,  5, -1},
        {  8, -1, -1,  4,  5, -1},
        { -1, -1,  6,  7, -1, -1},
        { -1, -1, -1,  7, -1, -1},
        {  8, -1, -1,  7, -1, -1},
        {  8, -1, -1, -1, -1, -1}
    };
    //valid final status : 4, 5, 8, 9
    private static boolean isValidStatus(int x) {
        return x == 3 || x == 4 || x == 7 || x == 8;
    }
    private static boolean isNotValidStatus(int x) {
        return x == -1;
    }
    public boolean isNumber(String s) {
        if (s == null) return false;
        int size = s.length();
        int currentStatus = 0;
        for (int i = 0; i < size; i++) {
            currentStatus = trans[currentStatus][kindOfChar(s.charAt(i))];
            if (isNotValidStatus(currentStatus)) return false;
        }
        return isValidStatus(currentStatus);
    }
}

```

##### *Method #3*
``` java
/*
 *Author: yeh
 *Time: 2017_08_05
 *Language: Java
 *
 */

public class Solution {
    //valis kinds:
    //1) (space) + float + (space)
    //2) (space) + float + e + integer + (space)
    //regex from : http://blog.csdn.net/fightforyourdream/article/details/12900751
    private static final String regex = "[-+]?(\\d+\\.?|\\.\\d+)\\d*(e[-+]?\\d+)?";
    public boolean isNumber(String s) {
        if (s == null) return false;
        return s.trim().matches(regex);
    }
}

```


