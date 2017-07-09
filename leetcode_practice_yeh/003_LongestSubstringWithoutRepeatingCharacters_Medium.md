

### Leetcode 3
#### [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters)
  
    Given a string, 
    find the length of the longest substring 
    without repeating characters.

**examples:**

    Given "pwwkew", the answer is "wke", with the length of 3. 
    Note that the answer must be a substring, 
    "pwke" is a subsequence and not a substring.
    
    Given "°¡°¡°¡"(not ASCII), the answer can't be got by the code the leetcode provide.
    Line 8: java.lang.ArrayIndexOutOfBoundsException: 21834
    So the input string would be made of ASCII character.

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_05
 *Language: Java
 *
 */
 

public class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s == null) return 0;
        int[] num = new int[256];
        char[] sarray = s.toCharArray();
        //double pointer
        int l = 0;
        int r = 0;
        int maxlength = 0;
        char ch;
        while(r < sarray.length) {
            ch = sarray[r];
            num[ch]++;
            while(num[ch] > 1) {
                num[sarray[l]]--;
                l++;
            }
            maxlength = Math.max(maxlength, r-l+1);
            r++;
        }
        return maxlength;
    }
}

```

