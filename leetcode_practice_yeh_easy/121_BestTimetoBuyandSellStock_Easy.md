

### Leetcode 121
#### [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock)

  

##### ***Problem:***

    Say you have an array for which the ith element is the price of a given stock on day i.

    If you were only permitted to complete at most one transaction 
    (ie, buy one and sell one share of the stock),
    design an algorithm to find the maximum profit.
    
    Note: gived array a[], return max of (a[j] - a[i]) when j >= i.
    

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
        int leftmin = Integer.MAX_VALUE;
        int maxprofit = 0;
        // [l, r], maxprofit
        // --> prices[l] = min(prices[0...r))
        for (int i = 0; i < prices.length; i++) {
            if (prices[i] < leftmin) {
                leftmin = prices[i];
            } else {
                maxprofit = Math.max(prices[i] - leftmin, maxprofit);
            }
        }
        return maxprofit;
    }
}


```


