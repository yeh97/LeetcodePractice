


### Leetcode 221
#### [Maximal Square](https://leetcode.com/problems/maximal-square)


##### ***Problem:***

    Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

##### ***Example:***

    Input: [["1"]]
        Output: 1

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_06
 *Language: Python3
 *
 */

class Solution:
    def maximalSquare(self, matrix):
        """
        :type matrix: List[List[str]]
        :rtype: int
        """
        if not matrix or len(matrix) == 0 or len(matrix[0]) == 0:
            return 0
        # dp[i, j] := maximal square when [i, j - 1] as Right_Bottom dot
        # dp[i, 0] := 0
        # matrix[i, j - 1] == 0 --> dp[i, j] = 0
        # matrix[i, j - 1] == 1 --> dp[i, j] = min(dp[i - 1, j], dp[i, j - 1], dp[i - 1, j - 1]) + 1
        dp = [0] + list(map(int, matrix[0]))
        lenm, lenn = len(matrix), len(matrix[0])
        maxsqsize, temp = int(1 in dp), 0
        for ii in range(1, lenm):
            for jj in range(1, lenn + 1):
                # prev : dp[ii - 1, jj - 1]
                prev, temp = temp, dp[jj]
                if matrix[ii][jj - 1] == '1':
                    dp[jj] = min(prev, dp[jj - 1], dp[jj]) + 1
                else:
                    dp[jj] = 0
            maxsqsize = max(maxsqsize, max(dp))
        return maxsqsize * maxsqsize

```

