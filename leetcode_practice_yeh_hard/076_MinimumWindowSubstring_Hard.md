

### Leetcode 76
#### [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring)

  

##### ***Problem:***

    Given a string S and a string T,
    find the minimum window in S which will contain all the characters in T in complexity O(n).
    
    If there is no such window in S that covers all characters in T, return the empty string "".

    If there are multiple such windows, 
    you are guaranteed that there will always be only one unique minimum window in S.


##### ***Example:***

    Input: "ADOBECODEBANC", "ABC"
        Output: "BANC"

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_07
 *Language: Java
 *
 */

public class Solution {
    public String minWindow(String s, String t) {
        if (s == null || t == null) return "";
        if (s.length() == 0 || t.length() == 0) return "";
        int needMatchNum = t.length();
        int[] charNum = new int[256];
        //if charNum[i] != minvalue : the num of (char) i in t - in s
        //charNum[i] == minvalue : (char) i isn't in t
        //assert (t.length() <= maxvalue && s.length() <= maxvalue)
        for (int i = t.length() - 1; i >= 0; i--) {
            charNum[t.charAt(i)]++;
        }
        for (int i = 0; i < 256; i++) {
            if (charNum[i] > 0) continue;
            charNum[i] = Integer.MIN_VALUE;
        }
        int sLength = s.length();
        char currentChar;
        //splid window : [winl, winr]
        //get first char s[winl] exist in t
        int winl = 0;
        while (winl < sLength && charNum[currentChar = s.charAt(winl)] == Integer.MIN_VALUE) {
            winl++;
        }
        if (winl >= sLength) return "";
        //the shorted window : [retl, retr]
        int retl = -Integer.MAX_VALUE;
        int retr = 0;
        //int retLength = 0; //retr - retl + 1
        for (int winr = winl; winr < sLength; winr++) {
            currentChar = s.charAt(winr);
            //currentChar not in t
            if (charNum[currentChar] == Integer.MIN_VALUE) continue;
            //charNum[i] : num of (char) i in t - in s
            charNum[currentChar]--;
            if (charNum[currentChar] >= 0) needMatchNum--;
            //not match whole t
            if (needMatchNum > 0) continue;
            //if winl == winr, loop must stop, so winl < sLength
            //get next char has been matched
            while (winl < sLength && charNum[currentChar = s.charAt(winl)] < 0) {
                if (charNum[currentChar = s.charAt(winl)] != Integer.MIN_VALUE) {
                    charNum[currentChar]++;
                }
                winl++;
            }
            if (winr - winl < retr - retl) {
                retl = winl;
                retr = winr;
            }
            //remove the char
            winl++;
            charNum[currentChar]++;
            if (charNum[currentChar] > 0) needMatchNum++;
            //get next char has been matched
            while (winl < sLength && charNum[currentChar = s.charAt(winl)] < 0) {
                if (charNum[currentChar = s.charAt(winl)] != Integer.MIN_VALUE) {
                    charNum[currentChar]++;
                }
                winl++;
            }
            if (winl > winr) winr = winr;
        }
        return (retl < 0) ? "" : s.substring(retl, retr + 1);
    }
}
```


