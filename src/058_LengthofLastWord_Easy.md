

### Leetcode 58
#### [Length of Last Word](https://leetcode.com/problems/length-of-last-word)

##### ***Problem:***

    Given a string s consists of upper/lower-case alphabets and empty space characters ' ', 
    return the length of last word in the string.

    If the last word does not exist, return 0.


##### ***Example:***
 
    Input: "a bb ccc"
    Ouput: 3
    

##### *Method: #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_02
 *Language: Java
 *
 */

public class Solution {
    public int lengthOfLastWord(String s) {
        if (s == null || s.length() == 0) return 0;
        int size = s.length();
        //get the end index of last word
        int end = size - 1;
        for (; end >= 0; end--) {
            if(s.charAt(end) != ' ') break;
        }
        //no char which != ' '
        if (end < 0) return 0;
        //get the previous of last word
        int start = end;
        for (; start >= 0; start--) {
            if (s.charAt(start) == ' ') break;
        }
        return end - start;
    }
}
```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_02
 *Language: Java
 *
 */

public class Solution {
    public int lengthOfLastWord(String s) {
        if (s == null) return 0;
        //"\\s+" means split by any continuous space
        String[] sSplit = s.split("\\s+");
        return sSplit.length == 0 ? 0 : sSplit[sSplit.length - 1].length();
    }
}

```

