

### Leetcode 151
#### [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string)

  

##### ***Problem:***

    Given an input string, reverse the string word by word.
    
##### ***Example:***

    Input: " b  a "
        Output: "a b"


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_01_29
 *Language: Java
 *
 */

public class Solution {
    public String reverseWords(String s) {
        // 2018/1/29 : 3ms
        // only one space is reserved between two word!
        if (s == null || s.length() == 0) return s;
        // split(ss) : ss("\\ ")(1 space) or ss("\\s+") (>=1 space)
        String[] str = s.trim().split("\\ ");
        StringBuilder res = new StringBuilder("");
        for (int i = str.length - 1; i >= 0; i--) {
            if (str[i].length() == 0) continue;
            res.append(str[i]);
            res.append(" ");
        }
        if (res.length() == 0) return "";
        res.deleteCharAt(res.length() - 1);
        return res.toString();
    }
}

```
