

### Leetcode 139
#### [Word Break](https://leetcode.com/problems/word-break)

  

##### ***Problem:***

    Given a non-empty string s and 
    a dictionary wordDict containing a list of non-empty words, 
    determine if s can be segmented into a space-separated sequence of one or more dictionary words.
    
    You may assume the dictionary does not contain duplicate words.

    
##### ***Example:***

    Input: "let", ["l", "t"]
        Output: false

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_26
 *Language: Java
 *
 */

class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        HashSet<String> dict = new HashSet<String>(wordDict);
        // assert s != null && s.length() > 0
        int n = s.length();
        // dp[i] : wordBreak(s.substring(0, i), wordDict)
        boolean[] dp = new boolean[n + 1];
        dp[0] = true;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j <= i; j++) {
                if (dp[j] && dict.contains(s.substring(j, i + 1))) {
                    dp[i + 1] = true;
                    break;
                }
            }
        }
        return dp[n];
    }
}

```


