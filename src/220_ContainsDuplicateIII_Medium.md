


### Leetcode 220
#### [Contains Duplicate III](https://leetcode.com/problems/contains-duplicate-iii)


##### ***Problem:***

    Given an array of integers, find out whether there are two distinct indices i and j in the array such that the absolute difference between nums[i] and nums[j] is at most t and the absolute difference between i and j is at most k.

##### ***Example:***

    Input: nums = [1,5,9,1,5,9], k = 2, t = 3
        Output: false

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_06
 *Language: Python3
 *
 */

class Solution:
    def containsNearbyAlmostDuplicate(self, nums, k, t):
        """
        :type nums: List[int]
        :type k: int
        :type t: int
        :rtype: bool
        """
        # |nums[i] - nums[j]| <= t -->
        # |floor(nums[i] / t) - floor(nums[j] / t)| <= 1
        if not nums or len(nums) < 2 or k < 1 or t < 0:
            return False
        ttmp, dicts = max(1, t), collections.OrderedDict()
        for ii, num in enumerate([num // ttmp for num in nums]):
            for key in (num - 1, num, num + 1):
                if key in dicts and abs(dicts[key] - nums[ii]) <= t:
                    return True
            dicts[num] = nums[ii]
            if ii >= k:
                dicts.popitem(last = False)
        return False

```

