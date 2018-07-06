


### Leetcode 213
#### [House Robber II](https://leetcode.com/problems/house-robber-ii)


##### ***Problem:***

    You are a professional robber planning to rob houses along a street.
    Each house has a certain amount of money stashed.
    All houses at this place are arranged in a circle.
    That means the first house is the neighbor of the last one.
    Meanwhile, adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.
    Given a list of non-negative integers representing the amount of money of each house,
    determine the maximum amount of money you can rob tonight without alerting the police.

##### ***Example:***

    Input: [1,2,3,1]
        Output: 4

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_04
 *Language: Python3
 *
 */

class Solution:
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums or len(nums) == 0:
            return 0
        def robList(numsList):
            """Leetcode 198"""
            # rob[i] : max_rob(rob i_th)
            # nrob[i] : max_rob(not rob i_th)
            rob, nrob = 0, 0
            for num in numsList:
                rob, nrob = nrob + num, max(rob, nrob)
            return max(rob, nrob)
        # rob : val if rob 0_th
        rob = robList(nums[2:len(nums)-1]) + nums[0]
        nrob = robList(nums[1:])
        return max(rob, nrob)

```

