

### Leetcode 87
#### [Scramble String](https://leetcode.com/problems/scramble-string)

  

##### ***Problem:***

    Given a string s1, 
    we may represent it as a binary tree by partitioning it to two non-empty substrings recursively.
    To scramble the string, 
    we may choose any non-leaf node and swap its two children.
    The time of swapping is not limited.
    
    Given two strings s1 and s2 of the same length, 
    determine if s2 is a scrambled string of s1.


##### ***Example:***

    Input: "a", "a"
        Output: true

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_09
 *Language: Java
 *
 */

public class Solution {
    public boolean isScramble(String s1, String s2) {
        // can cut s in any position
        // if s1.size != s2.size return false
        // for i = 1...n-1
        // isScramble(s1, s2) |= 
        // ( isScramble(s1.substring(0, i), s2.substring(0, i))
        // && isScramble(s1.substring(i, n), s2.substring(i, n)) )
        // || ( isScramble(s1.substring(i, n), s2.substring(0, n - i))
        // && isScramble(s1.substring(0, i), s2.substring(n - i, n)) )
        if (s1 == null || s2 == null) {
            return s1 == null && s2 == null;
        }
        int length = s1.length();
        if (length != s2.length()) return false;
        // dp[l][i1][i2] : 
        // isScramble(s1.substring(i1, i1 + l), s2.substring(i2, i2 + l))
        boolean[][][] dp = new boolean[length + 1][length][length];
        // l == 1, s.substring(i, i + l) = s.charAt(i)
        for (int i1 = 0; i1 < length; i1++) {
            for (int i2 = 0; i2 < length; i2++) {
                dp[1][i1][i2] = s1.charAt(i1) == s2.charAt(i2);
            }
        }
        for (int l = 2; l <= length; l++) {
            for (int i1 = 0; i1 <= length - l; i1++) {
                for (int i2 = 0; i2 <= length - l; i2++) {
                    for (int len = 1; len < l; len++) {
                        //l = len + (l - len)
                        //s(i, i + l) == s(i, i + len) + s(i + len, i + l)
                        dp[l][i1][i2] = 
                            (dp[len][i1][i2] && dp[l - len][i1 + len][i2 + len])
                            || (dp[len][i1][i2 + l - len] && dp[l - len][i1 + len][i2]);
                        if (dp[l][i1][i2]) break;
                    }
                }
            }
        }
        return dp[length][0][0];
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_09
 *Language: Java
 *
 */

public class Solution {
    public boolean isScramble(String s1, String s2) {
        // can cut s in any position
        // if s1.size != s2.size return false
        // for i = 1...n-1
        // isScramble(s1, s2) |= 
        // ( isScramble(s1.substring(0, i), s2.substring(0, i))
        // && isScramble(s1.substring(i, n), s2.substring(i, n)) )
        // || ( isScramble(s1.substring(i, n), s2.substring(0, n - i))
        // && isScramble(s1.substring(0, i), s2.substring(n - i, n)) )
        if (s1 == null || s2 == null) {
            return s1 == null && s2 == null;
        }
        int length = s1.length();
        if (length != s2.length()) return false;
        if (s1.equals(s2)) return true;
        if (!hasSameLowLetter(s1.toCharArray(), s2.toCharArray())) return false;
        for (int i = 1; i < length; i++) {
            if (isScramble(s1.substring(0, i), s2.substring(0, i)) 
                && isScramble(s1.substring(i, length), s2.substring(i, length))) return true;
            if (isScramble(s1.substring(i, length), s2.substring(0, length - i)) 
                && isScramble(s1.substring(0, i), s2.substring(length - i, length))) return true;
        }
        return false;
    }
    private boolean hasSameLowLetter(char[] s1, char[] s2) {
        //assert (s1 != null && s2 != null)
        //assert (Character.isLowerCase(s.charAt(i)))
        if (s1.length != s2.length) return false;
        int[] numLetter = new int[26];
        for (char ch : s1) {
            numLetter[ch - 'a']++;
        }
        for (char ch : s2) {
            numLetter[ch - 'a']--;
        }
        for (int num : numLetter) {
            if (num != 0) return false;
        }
        return true;
    }
}

```


