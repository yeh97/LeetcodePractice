


### Leetcode 215
#### [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array)


##### ***Problem:***

    Find the kth largest element in an unsorted array.
    Note that it is the kth largest element in the sorted order, not the kth distinct element.

##### ***Example:***

    Input: [3,2,3,1,2,4,5,5,6], 4
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
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        nums = sorted(nums, reverse=True)
        return nums[k - 1]

```

##### *Method #2*
``` python
/*
 *Author: yeh
 *Time: 2018_07_04
 *Language: Python3
 *
 */

class Solution:
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        # qsort method : descending order
        def swap(array, l, r):
            array[l], array[r] = array[r], array[l]
        def partition(array, l, r):
            swap(array, random.randint(l, r), r)
            par = array[r]
            i = l - 1
            for j in range(l, r):
                # descending order
                if array[j] >= par:
                    i += 1
                    swap(array, i, j)
            swap(array, i + 1, r)
            return i + 1
        
        x = partition(nums, 0, len(nums) - 1)
        if x == k - 1:
            return nums[x]
        elif x > k - 1:
            return self.findKthLargest(nums[:x], k)
        else:
            return self.findKthLargest(nums[x + 1:], k - x - 1)

```

