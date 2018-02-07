


### Leetcode 188
#### [Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv)

  

##### ***Problem:***

	Say you have an array for which the i-th element is the price of a given stock on day i.
	
	Design an algorithm to find the maximum profit. 
	You may complete at most k transactions.
	You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
	
##### ***Example:***

    Input: 2, [3, 30, 34, 5, 9, 0]
        Output: 35


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_07
 *Language: Java
 *
 */

class Solution {
    public int maxProfit(int k, int[] prices) {
        // 2018/2/7 : 3ms
        if (prices == null || prices.length < 2 || k < 1) return 0;
        // max num of independent transactions is half of time
        if (k >= prices.length / 2) {
            // Best Time to Buy and Sell Stock II
            int profit = 0;
            for (int i = 1; i < prices.length; i++) {
                profit += Math.max(0, prices[i] - prices[i - 1]);
            }
            return profit;
        }
        // dp_1[i][j] := maxProfit(j, prices[0...i])
        // dp_2[i][j] := maxProfit(j, prices[0...i]), transaction in i-th day
        // dp_1[i][j] = max(dp_1[i - 1][j], dp_2[i][j])
        // diff[i] := prices[i] - prices[i - 1]
        // dp_2[i][j] = max(dp_1[i - 1][j - 1] + max(diff[i], 0), dp_2[i - 1][j] + diff[i])
        int[] dp_1 = new int[k + 1];
        int[] dp_2 = new int[k + 1];
        for (int i = 1; i < prices.length; i++) {
            int diff = prices[i] - prices[i - 1];
            for (int j = k; j > 0; j--) {
                // dp_2[i][j] : dp_1[i - 1][j - 1],               dp_2[i - 1][j]
                dp_2[j] = Math.max(dp_1[j - 1] + Math.max(diff, 0), dp_2[j] + diff);
                // dp_1[i][j] : dp_1[i - 1][j], dp_2[i][j]
                dp_1[j] = Math.max(dp_1[j], dp_2[j]);
            }
        }
        return dp_1[k];
    }
}

```





