

### Leetcode 44
#### [Wildcard Matching](https://leetcode.com/problems/wildcard-matching)

  

##### ***Problem:***

    Implement wildcard pattern matching with support for '?' and '*'.
    '?' Matches any single character.
    '*' Matches any sequence of characters (including the empty sequence).
    
    
##### ***Example:***

    1) isMatch("aa","a") ? false
    2) isMatch("aa","aa") ? true
    3) isMatch("aaa","aa") ? false
    4) isMatch("aa", "*") ? true
    5) isMatch("aa", "a*") ? true
    6) isMatch("ab", "?*") ? true
    7) isMatch("aab", "c*a*b") ? false

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_29
 *Language: Java
 *
 */

public class Solution {
    //similar to leetcode 10 : Regular Expression Matching
    //DFS method :
    /*
    public boolean isMatch(char[] s, int is, char[] p, int ip) {
        //assert(s!=null && p!=null)
        if (ip >= p.length) return is >= s.length;
        if (p[ip] == '*') {
            for (int i = is - 1; i < s.length; i++) {
                if (isMatch(s, i+1, p, ip+1)) return true;
            }
            return false;
        }
        if (is<s.length && (p[ip]=='?' || p[ip]==s[is])) {
            return isMatch(s, is+1, p, ip+1);
        }
        return false;
    }
    */
    //DFS 1 will TLE
    //Input:　"aaabbbaabaaaaababaabaaabbabbbbbbbbaabababbabbbaaaaba", "a*******b"
    /*
    public boolean isMatch(String s, String p) {
        if (s==null || p==null) return s==null && p==null;
        return isMatch(s.toCharArray(), 0, p.toCharArray(), 0);
    }
    */
    //DFS 2 will TLE
    //Input :
    //"abbabaaabbabbaababbabbbbbabbbabbbabaaaaababababbbabababaabbababaabbbbbbaaaaba
    //babbbaabbbbaabbbbababababbaabbaababaabbbababababbbbaaabbbbbabaaaabbababbbbaababaab
    //bababbbbbababbbabaaaaaaaabbbbbaabaaababaaaabb",
    //"**aa*****ba*a*bb**aa*ab****a*aaaaaa***a*aaaa**bbabb*b*b**aaaaaaaa
    //a*a********ba*bbb***a*ba*bb*bb**a*b*bb"
    /*
    public boolean isMatch(String s, String p) {
        if (s==null || p==null) return s==null && p==null;
        char[] chsp = new char[p.length()];
        int length = chsp.length;
        //convert "**" to "*"
        //similar to KMP
        //split by '*', use KMP match every part
        for (int i = chsp.length - 1; i >= 0; i--) {
            chsp[--length] = p.charAt(i);
            if (p.charAt(i) == '*') {
                for (i--; i>=0 && p.charAt(i)=='*'; i--) {
                    //null
                }
                i++;
            }
        }
        return isMatch(s.toCharArray(), 0, chsp, length);
    }
    */
    //simplify DFS 2 to a function
    //using Recursive instead of Iteration
    //using Greedy : if match error, back to nearest '*'
    //AC
    public boolean isMatch(String s, String p) {
        int is = 0;
        int ip = 0;
        //start of the string matched by '*'
        int start = -1;
        int match = 0;
        int slength = s.length();
        int plength = p.length();
        while (is < slength) {
            if (ip<plength && (p.charAt(ip)=='?' || p.charAt(ip)==s.charAt(is))) {
                is++;
                ip++;
            } else if (ip<plength && p.charAt(ip)=='*') {
                match = is;
                start = ip;
                ip++;
            } else if (start != -1) {
                match++;
                is = match;
                ip = start + 1;
            } else {
                return false;
            }
        }
        while (ip<plength && p.charAt(ip)=='*') {
            ip++;
        }
        return (ip==plength);
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_07_30
 *Language: Java
 *
 */

public class Solution {
    //DP
    public boolean isMatch(String s, String p) {
        if (s==null || p==null) return s==null && p==null;
        boolean[][] dp = new boolean[2][p.length() + 1];
        dp[0][0] = true;
        for (int i = 1; i < dp[0].length; i++) {
            if (p.charAt(i - 1) == '*') {
                dp[0][i] = dp[0][i - 1];
            } else {
                break;
            }
        }
        int slength = s.length();
        for (int i = 1; i <= slength; i++) {
            for (int j = 1; j < dp[0].length; j++) {
                if (p.charAt(j - 1) == '?' || p.charAt(j - 1) == s.charAt(i - 1)) {
                    dp[1][j] = dp[0][j - 1];
                } else if (p.charAt(j - 1) == '*') {
                    dp[1][j] = dp[0][j] || dp[1][j - 1];
                } else {
                    dp[1][j] = false;
                }
            }
            for (int j = 0; j < dp[0].length; j++) {
                dp[0][j] = dp[1][j];
            }
        }
        return dp[0][dp[0].length - 1];
    }
}
```



