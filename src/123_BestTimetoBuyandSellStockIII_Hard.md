

### Leetcode 123
#### [Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii)

  

##### ***Problem:***

    Say you have an array for which the ith element is the price of a given stock on day i.

    Design an algorithm to find the maximum profit. 
    You may complete at most two transactions.

    You may not engage in multiple transactions at the same time 
    (ie, you must sell the stock before you buy again).


##### ***Example:***

    Input: [1,3,7,2,9]
        Output: 13

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_17
 *Language: Java
 *
 */

public class Solution {
    public int maxProfit(int[] prices) {
        // p[rr], p[mr], p[ml], p[ll]
        // rr >= mr >= ml >= ll
        // return max(p[rr] - p[mr] - p[ml] - p[ll])
        // buy1[i] : [0, i], buy first stock, max profit
        //        <--> min(p[j]) j in 0 : i
        //        <--> buy1[i] = max(buy1[i - 1], -p[i])
        // sell1[i] : [0, i], sell fitst stock, max profit
        //        <--> max(p[j] - p[k]), 0 <= k <= j <= i
        //        <--> sell1[i] = max(sell1[i - 1], buy1[i - 1] + p[i])
        // buy2[i] : [0, i], buy second stock, max profit
        //        <--> max(-p[j] + p[k] - p[l]), 0 <= l <= k <= j <= i
        //        <--> buy2[i] = max(buy2[i - 1], sell1[i - 1] - p[i])
        // sell2[i] : [0, i], sell second stock, max profit
        //        <--> max(p[j] - p[k] + p[l] - p[m]), 0 <= m <= l <= k <= j <= i
        //        <--> sell2[i] = max(sell2[i - 1], buy2[i - 1] + p[i])
        // p[i] -> buy1[i] -> sell1[i] --> buy2[i] --> sell2[i]
        // if update in order : sell2, buy2, sell1, buy1, O(1) space, O(n) times
        // <--> return sell2[n - 1]
        if (prices == null || prices.length == 0) return 0;
        int buy1, buy2, sell1, sell2;
        buy1 = buy2 = Integer.MIN_VALUE;
        sell1 = sell2 = 0;
        for (int i = 0; i < prices.length; i++) {
            sell2 = Math.max(sell2, buy2 + prices[i]);
            buy2 = Math.max(buy2, sell1 - prices[i]);
            sell1 = Math.max(sell1, buy1 + prices[i]);
            buy1 = Math.max(buy1, -prices[i]);
        }
        return sell2;
    }
}

```


