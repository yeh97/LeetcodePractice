


### Leetcode 216
#### [Combination Sum III](https://leetcode.com/problems/combination-sum-iii)


##### ***Problem:***

    Find all possible combinations of k numbers that add up to a number n,
    given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

##### ***Example:***

    Input: k = 3, n = 9
        Output: [[1,2,6], [1,3,5], [2,3,4]]

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_04
 *Language: Python3
 *
 */

class Solution:
    def combinationSum3(self, k, n):
        """
        :type k: int
        :type n: int
        :rtype: List[List[int]]
        """
        # C(9, 4) = C(9, 5) = 126
        if k > 9 or n > 45 or n <= 0 or n < k * (k + 1) / 2:
            return []
        res = []
        def searchDFS(start, cnt, num, nums):
            if cnt == k and num == n:
                res.append(nums)
            elif cnt < k and num < n:
                for ii in range(start + 1, 10):
                    searchDFS(ii, cnt + 1, num + ii, nums + [ii])
        searchDFS(0, 0, 0, [])
        return res

```

