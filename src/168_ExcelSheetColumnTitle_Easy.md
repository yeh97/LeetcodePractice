


### Leetcode 168
#### [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title)

  

##### ***Problem:***

    Given a positive integer, 
    return its corresponding column title as appear in an Excel sheet.
    
##### ***Example:***

    Input: 27
        Output: "AA"


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_04
 *Language: Java
 *
 */

class Solution {
    public String convertToTitle(int n) {
        // 2018/2/4 : 0ms
        StringBuilder res = new StringBuilder("");
        for (int i = n; i > 0; i = (i - 1) / 26) {
            res.append((char) ('A' + (i - 1) % 26));
        }
        return res.reverse().toString();
    }
}



```


