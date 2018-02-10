


### Leetcode 205
#### [Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings)

  

##### ***Problem:***

	Given two strings s and t, 
	determine if they are isomorphic.

	Two strings are isomorphic 
	if the characters in s can be replaced to get t.

	All occurrences of a character must be replaced with another character 
	while preserving the order of characters. 
	No two characters may map to the same character but a character may map to itself.
	
##### ***Example:***

    Input: "foo", "bar"
        Output: false

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_10
 *Language: Java
 *
 */

class Solution {
    public boolean isIsomorphic(String s, String t) {
        // 2018/2/10 : 3ms
        if (s == null || t == null) return s == null && t == null;
        if (s.length() != t.length()) return false;
        if (s.equals(t)) return true;
        int[] maps = new int[256];
        int[] mapt = new int[256];
        int[] tmap = new int[256];
        char[] strs = s.toCharArray();
        char[] strt = t.toCharArray();
        for (int i = 0; i < strs.length; i++) {
            if (maps[strs[i]] != mapt[strt[i]]) return false;
            maps[strs[i]] = mapt[strt[i]] = i + 1;
        }
        return true;
    }
}

```
