

### Leetcode 16
#### [3Sum Closest](https://leetcode.com/problems/3sum-closest)

    Given an array S of n integers, 
    find three integers in S 
    such that the sum is closest to a given number, target. 
    
    Return the sum of the three integers. 
    
    You may assume that each input would have exactly one solution.

    
**Example:**

    Input S = [-1, 2, 1, -4], target = 1
    Ouput : 2  (-1 + 2 + 1 = 2)


``` java
/*
 *Author: yeh
 *Time: 2017_07_09
 *Language: Java
 *
 */

public class Solution {
    public int threeSumClosest(int[] nums, int target) {
        if(nums==null || nums.length<3) return 0;
        int ret;
        int size = nums.length;
        Arrays.sort(nums);
        //some special cases
        if(nums.length == 3) return nums[0] + nums[1] + nums[2];
        if((ret = nums[0]+nums[1]+nums[2]) > target) return ret;
        if((ret = nums[size-3]+nums[size-2]+nums[size-1]) < target) return ret;
        //index of the three number
        int left;
        int mid;
        int right;
        //sum of the three number
        //the cloest with target would be returned
        int sum;
        //the abs(tar-sum) may overflow if using int
        long del = Long.MAX_VALUE;
        for(left=0; left<size-2; left++) {
            //avoid repeat operation
            if(left>0 && nums[left]==nums[left-1]) continue;
            mid = left + 1;
            right = size - 1;
            while(right > mid) {
                sum = nums[left] + nums[mid] + nums[right];
                if(sum > target) {
                    if((long)(sum) - (long)(target) < del) {
                        del = (long)(sum) - (long)(target);
                        ret = sum;
                    }
                    right--;
                }else if(sum < target) {
                    if((long)(target) - (long)(sum) < del) {
                        del = (long)(target) - (long)(sum);
                        ret = sum;
                    }
                    mid++;
                }else{//sum == target
                    ret = sum;
                    return ret;
                }
            }
        }
        return ret;
    }
}


```
