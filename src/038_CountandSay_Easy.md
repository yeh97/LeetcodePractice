

### Leetcode 38
#### [Count and Say](https://leetcode.com/problems/count-and-say)

##### ***Problem:***

    The count-and-say sequence is the sequence of integers 
    with the first five terms as following:
        1:      1
        2:      11
        3:      21
        4:      1211
        5:      111221
        
    1 is read off as "one 1" or 11.
    11 is read off as "two 1s" or 21.
    21 is read off as "one 2, then one 1" or 1211
    
    Given an integer N, 
    generate the Nth term of the count-and-say sequence.


##### ***Example:***
 
    Input: 5
    Ouput: "111221"
    

##### *Method: #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_28
 *Language: Java
 *
 */

public class Solution {
    public String countAndSay(int n) {
        if (n <= 0) return "";
        StringBuilder ret = new StringBuilder("1");
        for (int i = 1; i < n; i++) {
            ret = nextCountSay(ret);
        }
        return ret.toString();
    }
    private StringBuilder nextCountSay(StringBuilder s) {
        //assert (s!=null && s.length()>0)
        //s is made of letter '0'...'9'
        StringBuilder ret = new StringBuilder();
        int length = s.length();
        int sameLetter;
        char currentCh;
        for (int i = 0; i< length; i++) {
            sameLetter = 1;
            currentCh = s.charAt(i);
            for (i++; i < length && currentCh == s.charAt(i); i++) {
                sameLetter++;
            }
            i--;
            ret.append(String.valueOf(sameLetter) + currentCh);
        }
        return ret;
    }
}

```

