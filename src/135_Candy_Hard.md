

### Leetcode 135
#### [Candy](https://leetcode.com/problems/candy)

  

##### ***Problem:***

    There are N children standing in a line.
    Each child is assigned a rating value.

    You are giving candies to these children subjected to the following requirements:
    1) Each child must have at least one candy.
    2) Children with a higher rating ( > ) get more candies than their neighbors.
    
    What is the minimum candies you must give?

    
##### ***Example:***

    Input: [1,2,2]
        Output: 4

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_23
 *Language: Java
 *
 */

class Solution {
    public int candy(int[] ratings) {
        if (ratings == null || ratings.length == 0) return 0;
        int[] cost = new int[ratings.length];
        Arrays.fill(cost, 1);
        for (int i = 1; i < ratings.length; i++) {
            if (ratings[i] > ratings[i - 1]) {
                cost[i] = 1 + cost[i - 1];
            }
        }
        for (int i = ratings.length - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
                cost[i] = Math.max(cost[i], 1 + cost[i + 1]);
            }
        }
        int sum = 0;
        for (int candy : cost) {
            sum += candy;
        }
        return sum;
    }
}

```


