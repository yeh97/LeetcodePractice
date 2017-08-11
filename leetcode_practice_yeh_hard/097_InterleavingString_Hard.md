

### Leetcode 97
#### [Interleaving String](https://leetcode.com/problems/interleaving-string)

  

##### ***Problem:***

    Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.


##### ***Example:***

    Input: "aabcc", "dbbca", "aadbbcbcac"
        Output: true
    Input: "aabcc", "dbbca", "aadbbbaccc"
	Output: false

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_11
 *Language: Java
 *
 */

public class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        // dp[i][j] : 
        // isInterleave(s1.substring(0, i), s2.substring(0, j), 
        // s3.substring(0, i + j))
        if (s3 == null) return s1 == null && s2 == null;
        if (s1 == null || s1.length() == 0) return s3.equals(s2);
        if (s2 == null || s3.length() == 0) return s3.equals(s1);
        if (s3.length() != s1.length() + s2.length()) return false;
        boolean[][] dp = new boolean[s1.length() + 1][s2.length() + 1];
        dp[0][0] = true;
        for (int i = 1; i < dp.length; i++) {
            if (!dp[i - 1][0]) break;
            dp[i][0] = s1.charAt(i - 1) == s3.charAt(i - 1);
        }
        for (int j = 1; j < dp[0].length; j++) {
            if (!dp[0][j - 1]) break;
            dp[0][j] = s2.charAt(j - 1) == s3.charAt(j - 1);
        }
        for (int i = 1; i < dp.length; i++) {
            for (int j = 1; j < dp[0].length; j++) {
                dp[i][j] = ((dp[i - 1][j] && s1.charAt(i - 1) == s3.charAt(i + j - 1)) 
                            || (dp[i][j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1)));
            }
        }
        return dp[s1.length()][s2.length()];
    }
}

```


