


### Leetcode 209
#### [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum)


##### ***Problem:***

    Given an array of n positive integers and a positive integer s,
    find the minimal length of a contiguous subarray of which the sum >= s.
    If there isn't one, return 0 instead.

##### ***Example:***

    Input: s = 7, nums = [2,3,1,2,4,3]
        Output: 2

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_03
 *Language: Python3
 *
 */

class Solution:
    def minSubArrayLen(self, s, nums):
        """
        :type s: int
        :type nums: List[int]
        :rtype: int
        """
        minLen = len(nums) + 1
        curSum, pl = 0, 0
        for pr in range(len(nums)):
            curSum += nums[pr]
            while curSum >= s:
                minLen = min(minLen, pr - pl + 1)
                curSum -= nums[pl]
                pl += 1
        return 0 if minLen > len(nums) else minLen

```

