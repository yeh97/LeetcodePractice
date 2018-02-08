

### Leetcode 14
#### [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix)

    Write a function to 
    find the longest common prefix string amongst an array of strings.
    

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_09
 *Language: Java
 *
 */

public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs==null || strs.length==0) return "";
        char[] ret = strs[0].toCharArray();
        //the longestCommonPrefix 's index in ret
        int end = ret.length;
        for(int i=1; i<strs.length; i++) {
            //avoid ArrayIndexOutOfBounds
            end = Math.min(strs[i].length(), end);
            //get longestCommonPrefix between ret and strs[i]
            for(int j=0; j<end; j++) {
                if(ret[j] == strs[i].charAt(j)) continue;
                end = j;
                break;
            }
        }
        return new String(ret, 0, end);
    }
}

```
