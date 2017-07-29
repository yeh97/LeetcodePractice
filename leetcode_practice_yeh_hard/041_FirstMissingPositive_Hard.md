

### Leetcode 41
#### [First Missing Positive](https://leetcode.com/problems/first-missing-positive)

  

##### ***Problem:***

    Given an unsorted integer array, 
    find the first missing positive integer.
    
##### ***Example:***

    Input: [1,2,0]
        Output: 3
    Input: [3,4,-1,1]
        Output: 2

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_29
 *Language: Java
 *
 */

public class Solution {
    public int firstMissingPositive(int[] nums) {
        if (nums==null || nums.length==0) return 1;
        //the answer must <= nums.length + 1
        //O(n) spaces
        int[] map = new int[nums.length + 1];
        for (int num : nums) {
            if (num > 0 && num <= nums.length) {
                map[num] = 1;
            }
        }
        for (int i = 1; i < map.length; i++) {
            if (map[i] == 0) return i;
        }
        return nums.length + 1;
    }
}

```


##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_07_29
 *Language: Java
 *
 */

public class Solution {
    public int firstMissingPositive(int[] nums) {
        if (nums==null || nums.length==0) return 1;
        //O(1) spaces
        for (int i = 0; i < nums.length; i++) {
            //target : 
            //(nums[i] > 0 && nums[i] <= nums.length) <-> nums[i] = i + 1;
            //but should avoid :
            //0 < nums[i]==nums[j] <= nums.length, i<j
            while (nums[i] > 0 && nums[i] <= nums.length 
                  && nums[nums[i] - 1] != nums[i]) {
                swap(nums, i, nums[i] - 1);
            }
        }
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != i + 1) return i + 1;
        }
        return nums.length + 1;
    }
    private void swap(int[] a, int i, int j) {
        //assert (a!=null && i>=0 && j>=0 && i<a.length && j<a.length)
        int t = a[i];
        a[i] = a[j];
        a[j] = t;
    }
}

```

