


### Leetcode 171
#### [Excel Sheet Column Number](https://leetcode.com/problems/excel-sheet-column-number)

  

##### ***Problem:***

    Given a column title as appear in an Excel sheet, 
    return its corresponding column number.
    
##### ***Example:***

    Input: "AA"
        Output: 27


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_04
 *Language: Java
 *
 */

class Solution {
    public int titleToNumber(String s) {
        // 2018/2/4 : 2ms
        if (s == null) return 0;
        int res = 0;
        for (char ch : s.toCharArray()) {
            res *= 26;
            res += ch - 'A' + 1;
        }
        return res;
    }
}


```


