

### Leetcode 131
#### [Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning)

  

##### ***Problem:***

    Given a string s, 
    partition s such that every substring of the partition is a palindrome.

    Return all possible palindrome partitioning of s.

    
##### ***Example:***

    Input: "aba"
        Output: [["a","b","a"], ["aba"]]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_23
 *Language: Java
 *
 */

class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> ret = new ArrayList<List<String>>();
        if (s == null || s.length() == 0) return ret;
        int n = s.length();
        // dp[i][j] : s.substring(i, j + 1) is Palindrome
        boolean[][] dp = new boolean[n][n];
        for (int i = n - 1; i >= 0; i--) {
            for (int j = i; j < n; j++) {
                if (i == j) {
                    dp[i][j] = true;
                } else {
                    if (s.charAt(i) == s.charAt(j)) {
                        if (j == i + 1 || dp[i + 1][j - 1]) {
                            dp[i][j] = true;
                        }
                    }
                }
            }
        }
        // DFS
        partitionDfs(s, dp, 0, n, new ArrayList<String>(), ret);
        return ret;
    }
    private void partitionDfs(String s, boolean[][] dp, int cur, int n,
                              List<String> t, List<List<String>> list) {
        if (cur == n) {
            list.add(new ArrayList<String>(t));
        } else {
            for (int j = cur; j < n; j++) {
                if (!dp[cur][j]) continue;
                t.add(s.substring(cur, j + 1));
                partitionDfs(s, dp, j + 1, n, t, list);
                t.remove(t.size() - 1);
            }
        }
    }
}

```


