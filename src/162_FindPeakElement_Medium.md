


### Leetcode 162
#### [Find Peak Element](https://leetcode.com/problems/find-peak-element)

  

##### ***Problem:***

    A peak element is an element that is greater than its neighbors.
    Given an input array where num[i] ≠ num[i+1], find a peak element and return its index.
    The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.
    You may imagine that num[-1] = num[n] = -∞.
    
##### ***Example:***

    Input: [1,2,3,1]
        Output: 2


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_01_31
 *Language: Java
 *
 */

class Solution {
    public int findPeakElement(int[] nums) {
        if (nums == null || nums.length < 2) return 0;
        for (int i = 0; i < nums.length; i++) {
            if ((i == 0 || nums[i] > nums[i - 1]) && (i == nums.length - 1 || nums[i] > nums[i + 1])) return i;
        }
        return nums.length - 1;
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2018_01_31
 *Language: Java
 *
 */

class Solution {
    public int findPeakElement(int[] nums) {
        if (nums == null || nums.length < 2) return 0;
        int l = 0;
        int r = nums.length - 1;
        while (l + 1 < r) {
            int m = l + (r - l) / 2;
            if (nums[m] < nums[m - 1]) {
                r = m;
            } else if (nums[m] < nums[m + 1]) {
                l = m;
            } else {
                return m; // the peak
            }
        }
        return nums[l] < nums[r] ? r : l;
    }
}

```
