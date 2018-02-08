

### Leetcode 122
#### [Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii)

  

##### ***Problem:***

    Say you have an array for which the ith element is the price of a given stock on day i.

    Design an algorithm to find the maximum profit. 
    You may complete as many transactions as you like 
    (ie, buy one and sell one share of the stock multiple times). 
    
    However, you may not engage in multiple transactions at the same time 
    (ie, you must sell the stock before you buy again).
    
    Note : gived array a[], return max of (a[b[k]] - a[b[k - 1] + ... + a[b[1]] - a[b[0]]) when 0 <= ... b[i] <= b[i + 1] ... < a.length.
    

##### ***Example:***

    Input: [1,3,7,5]
        Output: 6

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_15
 *Language: Java
 *
 */

public class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) return 0;
        int profit = 0;
        for (int i = 1; i < prices.length; i++) {
            profit += Math.max(0, prices[i] - prices[i - 1]);
        }
        return profit;
    }
}


```


