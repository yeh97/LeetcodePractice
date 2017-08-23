

### Leetcode 132
#### [Palindrome Partitioning II](https://leetcode.com/problems/palindrome-partitioning-ii)

  

##### ***Problem:***

    Given a string s, 
    partition s such that every substring of the partition is a palindrome.

    Return the minimum cuts needed for a palindrome partitioning of s.

    
##### ***Example:***

    Input: "aba"
        Output: 0

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_23
 *Language: Java
 *
 */

class Solution {
    public int minCut(String s) {
        if (s == null || s.length() == 0) return 0;
        int n = s.length();
        char[] chs = s.toCharArray();
        // dp[i][j] : s.substring(i, j + 1) is Palindrome
        boolean[][] dp = new boolean[n][n];
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
        }
        for (int i = n - 1; i >= 0; i--) {
            for (int j = i + 1; j < n; j++) {
                dp[i][j] = chs[i] == chs[j]
                    && (j == i + 1 || dp[i + 1][j - 1]);
            }
        }
        // cut[i] : minCut(s.substring(0, i))
        int[] cut = new int[n + 1];
        for (int i = -1; i < n; i++) {
            cut[i + 1] = i;
            for (int j = i; j >= 0; j--) {
                if (!dp[j][i]) continue;
                cut[i + 1] = Math.min(cut[i + 1], 1 + cut[j]);
            }
        }
        return cut[n];
    }
}


```


