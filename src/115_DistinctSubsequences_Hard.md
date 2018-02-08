

### Leetcode 115
#### [Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences)

  

##### ***Problem:***

    Given a string S and a string T, 
    count the number of distinct subsequences of S which equals T.

    A subsequence of a string is a new string 
    which is formed from the original string by deleting some (can be none) of the characters 
    without disturbing the relative positions of the remaining characters. 
    (ie, "ACE" is a subsequence of "ABCDE" while "AEC" is not)


##### ***Example:***

    Input: "aa", "a"
        Output: 2

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_14
 *Language: Java
 *
 */

public class Solution {
    public int numDistinct(String s, String t) {
        if (t == null || t.length() == 0) return 1;
        if (s == null || s.length() == 0) return 0;
        // dp[i][j] : 
        // numDistinct(s.substring(0, i), t.substring(0, j))
        // string.substring(0,0) <--> null
        char[] chss = s.toCharArray();
        char[] chst = t.toCharArray();
        int[][] dp = new int[chss.length + 1][chst.length + 1];
        // numDistinct(null, str) = 0
        // numDistinct(str, null) = 1
        // numDistinct(null, null) = 1
        for (int i = 0; i < dp.length; i++) {
            dp[i][0] = 1;
        }
        for (int i = 1; i < dp.length; i++) {
            for (int j = 1; j < dp[0].length; j++) {
                if (chss[i - 1] == chst[j - 1]) {
                    // if the subsequence contains s[i - 1], --> dp[i - 1][j - 1]
                    // else, --> dp[i - 1][j]
                    dp[i][j] = dp[i - 1][j] + dp[i - 1][j - 1];
                } else {
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }
        return dp[chss.length][chst.length];
    }
}

```


