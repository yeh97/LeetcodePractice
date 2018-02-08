

### Leetcode 91
#### [Decode Ways](https://leetcode.com/problems/decode-ways)

  

##### ***Problem:***

    A message containing letters from A-Z is being encoded to numbers using the following mapping:
    'A' -> 1 ... 'Z' -> 26
    
    Given an encoded message containing digits,
    determine the total number of ways to decode it.

##### ***Example:***

    Input: "1010"
        Output: 1

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_09
 *Language: Java
 *
 */

public class Solution {
    public int numDecodings(String s) {
        // assert (s[i] >= '0' && s[i] <= '9')
        if (s == null || s.length() == 0) return 0;
        if (s.charAt(0) == '0') return 0;
        int size = s.length();
        char preChar = s.charAt(0);
        // dp[i] = numDecodings(s.substring(0, i))
        int[] dp = new int[size + 1];
        dp[0] = dp[1] = 1;
        for (int i = 1; i < size; i++) {
            if (s.charAt(i) == '0') {
                // "00" isn't in map
                if (preChar == '0') return 0;
                if (preChar < '3') dp[i + 1] = dp[i - 1];
            } else {
                dp[i + 1] = dp[i];
                // "01", "02" isn't in map
                if (preChar != '0' && (preChar - '0') * 10 + (s.charAt(i) - '0') <= 26) {
                    dp[i + 1] += dp[i - 1];
                }
            }
            preChar = s.charAt(i);
        }
        return dp[size];
    }
}
```


