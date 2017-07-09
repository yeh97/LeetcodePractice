

##### Leetcode 5
##### [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring)

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

###### **Example:**
    Input: "babad"
    Output: "bab"
    Note: "aba" is also a valid answer.
###### **Example:**
    Input: "cbbd"
    Output: "bb"

``` java
/*
 *Author: yeh
 *Time: 2017_07_07
 *Language: Java
 *
 */
public class Solution {
    //Manacher
    public static final char addch = '\t';
    public String longestPalindrome(String s) {
        if(s == null) return null;
        
        char[] sarray = new char[2*s.length()+1];
        sarray[0] = addch;
        for(int i=0; i<s.length(); i++) {
            sarray[i<<1|1] = s.charAt(i);
            sarray[(i+1)<<1] = addch;
        }
        //p[i] == the Palindromic's radius when sarray[i] is the center(contain itself)
        int[] p = new int[sarray.length];
        int maxr = 0;
        int id = -1;
        for(int i=0; i<sarray.length; i++) {
            //2*id-i is the mirror of i about id
            p[i] = maxr>i ? Math.min(p[2*id-i], maxr-i) : 1;
            while(i-p[i]>=0 && i+p[i]<sarray.length 
                  && sarray[i-p[i]]==sarray[i+p[i]]) {
                p[i]++;
            }
            if(i+p[i] > maxr) {
                maxr = p[i]+i;
                id = i;
            }
        }
        //find max in p
        int maxlen = 0;
        int maxindex = 0;
        for(int i=0; i<p.length; i++) {
            if(p[i] > maxlen) {
                maxlen = p[i];
                maxindex = i;
            }
        }
        
        return s.substring((maxindex+1-maxlen)/2, (maxindex-1+maxlen)/2);
    }
}
```

