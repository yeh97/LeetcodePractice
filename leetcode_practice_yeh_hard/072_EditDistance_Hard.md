

### Leetcode 72
#### [Edit Distance](https://leetcode.com/problems/edit-distance)

  

##### ***Problem:***

    Given two words word1 and word2, find the minimum number of steps 
    required to convert word1 to word2. (each operation is counted as 1 step.)
    
    You have the following 3 operations permitted on a word:
    a) Insert a character; b) Delete a character; c) Replace a character


##### ***Example:***

    Input: "", ""
        Output: 0

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_07
 *Language: Java
 *
 */

public class Solution {
    public int minDistance(String word1, String word2) {
        //(1 -> 2) <--> (2 -> 1)
        if (word1 == null || word1.length() == 0) {
            return word2 == null ? 0 : word2.length();
        }
        if (word2 == null || word2.length() == 0) {
            return word1 == null ? 0 : word1.length();
        }
        //dp[i][j] : minDitance(word1.substring(i), word2.substring(j))
        int[][] dp = new int[word1.length() + 1][word2.length() + 1];
        for (int i = 0; i < dp.length; i++) {
            dp[i][0] = i;
        }
        for (int j = 0; j < dp[0].length; j++) {
            dp[0][j] = j;
        }
        //three convert method : insert, delete, replace
        //dp[i][j] = min{ dp[i - 1][j] + 1, dp[i][j - 1] + 1,
        //dp[i - 1][j - 1] + (word1[i - 1] == word2[j - 1] ? 0 : 1) }
        //(word1[i - 1] == word2[j - 1]) <--> dp[i][j] = dp[i - 1][j - 1]
        for (int i = 1; i < dp.length; i++) {
            for (int j = 1; j < dp[0].length; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = 1 + Math.min(dp[i - 1][j - 1],
                                            Math.min(dp[i][j - 1], dp[i - 1][j]));
                }                
            }
        }
        return dp[dp.length - 1][dp[0].length - 1];
    }
}

```


