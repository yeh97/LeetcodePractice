


### Leetcode 164
#### [Maximum Gap](https://leetcode.com/problems/maximum-gap)

  

##### ***Problem:***

    Given an unsorted array, find the maximum difference between the successive elements in its sorted form.
	Try to solve it in linear time/space.
	Return 0 if the array contains less than 2 elements.
	You may assume all elements in the array are non-negative integers and fit in the 32-bit signed integer range.
    
##### ***Example:***

    Input: [4,5,6,7,7,0,1,2,4,4,4]
        Output: 2


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_01
 *Language: Java
 *
 */

class Solution {
    public int maximumGap(int[] nums) {
        // 2018/2/1 : 4ms
        // Bucket sort
        if (nums == null || nums.length < 2) return 0;
        // find max(nums), min(nums)
        int maxv = nums[0], minv = nums[0];
        for (int i = 1; i < nums.length; i++) {
            maxv = Math.max(maxv, nums[i]);
            minv = Math.min(minv, nums[i]);
        }
        // nums have same element
        if (maxv == minv) return 0;
        // bucket partition
        // size : floor((max - min) / (length - 1)), size > 0
        // --> maximun diff in diff bucket
        // or every bucket have a elem --> num of elem in bucket > nums.length
        int bucket_size = Math.max(1, (maxv - minv) / (nums.length - 1));
        // num : floor((maxv - minv) / bucket_size) + 1
        // minv..., minv + size..., ..., minv + (n - 1) * size..maxv
        int bucket_num = (maxv - minv) / bucket_size + 1;
        // put elem into bucket, only save max(bucket), min(bucket)
        int[] bucket_max = new int[bucket_num];
        int[] bucket_min = new int[bucket_num];
        for (int i = 0; i < bucket_num; i++) {
            bucket_max[i] = -1;
            bucket_min[i] = Integer.MAX_VALUE;
        }
        for (int i = 0; i < nums.length; i++) {
            int id = (nums[i] - minv) / bucket_size;
            bucket_max[id] = Math.max(bucket_max[id], nums[i]);
            bucket_min[id] = Math.min(bucket_min[id], nums[i]);
        }
        // find maximum diff from near not-empty bucket
        // minv must in bucket_min[0], so bucket(0).isempty is false
        int res = 0;
        int pre_max = bucket_max[0];
        for (int i = 1; i < bucket_num; i++) {
            // empty bucket
            if (bucket_min[i] == Integer.MAX_VALUE) continue;
            res = Math.max(res, bucket_min[i] - pre_max);
            pre_max = bucket_max[i];
        }
        return res;
    }
}

```
