

### Leetcode 128
#### [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence)

  

##### ***Problem:***

    Given an unsorted array of integers,
    find the length of the longest consecutive elements sequence.

    
##### ***Example:***

    Input: [4,100,2,1,3,200]
        Output: 4

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_22
 *Language: Java
 *
 */

class Solution {
    public int longestConsecutive(int[] nums) {
        // map[i] : 
        // The longest consecutive elements sequence contains i in nums
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        int ret = 0;
        int leftLength, rightLength;
        int curLength;
        for (int val : nums) {
            if (map.containsKey(val)) continue;
            leftLength = map.containsKey(val - 1) ? map.get(val - 1) : 0;
            rightLength = map.containsKey(val + 1) ? map.get(val + 1) : 0;
            curLength = leftLength + rightLength + 1;
            map.put(val, curLength);
            // update border
            map.put(val - leftLength, curLength);
            map.put(val + rightLength, curLength);
            ret = Math.max(curLength, ret);
        }
        return ret;
    }
}

```


