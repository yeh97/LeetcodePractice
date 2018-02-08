

### Leetcode 134
#### [Gas Station](https://leetcode.com/problems/gas-station)

  

##### ***Problem:***

    There are N gas stations along a circular route, 
    where the amount of gas at station i is gas[i].

    You have a car with an unlimited gas tank 
    and it costs cost[i] of gas to travel from station i to its next station (i+1).
    You begin the journey with an empty tank at one of the gas stations.

    Return the starting gas station's index 
    if you can travel around the circuit once, 
    otherwise return -1.

    
##### ***Example:***

    Input: [1,2], [0,3]
        Output: 0

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_23
 *Language: Java
 *
 */

class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        // t[i] = g[i] - c[i], return i : 
        // t[i] ... + t[j] >= 0, j = i, ... , i - 1
        // if t[i] + ... t[j] < 0, 
        // t[i] + ...t[k] >= 0, k in i to j
        // --> k in i to j, t[k] + ...t[j] < 0
        // --> if sum(t[i]) >= 0, the index exist
        if (gas == null || cost == null) return -1;
        if (gas.length == 0 || cost.length == 0) return -1;
        if (gas.length != cost.length) return -1;
        int t = 0;
        int total = 0;
        int curGas = 0;
        int start = 0;
        for (int i = 0; i < gas.length; i++) {
            t = gas[i] - cost[i];
            total += t;
            if (curGas < 0) {
                curGas = t;
                start = i;
            } else {
                curGas += t;
            }
        }
        return total < 0 ? -1 : start;
    }
}


```


