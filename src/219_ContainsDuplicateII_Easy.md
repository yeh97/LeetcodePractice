


### Leetcode 219
#### [Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii)

  

##### ***Problem:***

    Given an array of integers and an integer k,
    find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.


##### ***Example:***

    Input: [1,2,3,1,2,3], 2
        Output: false

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_05
 *Language: Python3
 *
 */

class Solution:
    def containsNearbyDuplicate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """
        pre_index = {}
        for ii, val in enumerate(nums):
            if val in pre_index and ii - pre_index[val] <= k:
                return True
            else:
                pre_index[val] = ii
        return False

```
