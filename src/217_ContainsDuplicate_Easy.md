


### Leetcode 217
#### [Contains Duplicate](https://leetcode.com/problems/contains-duplicate)

  

##### ***Problem:***

    Given an array of integers, find if the array contains any duplicates.
    Your function should return true if any value appears at least twice in the array,
    and it should return false if every element is distinct.

##### ***Example:***

    Input: [1,2,3,1]
        Output: true

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_04
 *Language: Python3
 *
 */

class Solution:
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        return len(set(nums)) != len(nums)

```
