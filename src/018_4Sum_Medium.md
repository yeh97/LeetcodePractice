

### Leetcode 18
#### [4Sum](https://leetcode.com/problems/4sum)

    Given an array S of n integers, 
    are there elements a, b, c, and d in S 
    such that a + b + c + d = target? 
    
    Find all unique quadruplets in the array 
    which gives the sum of target.

**Note:**

    The solution set must not contain duplicate quadruplets.

    
**Example:**

    Input: S = [1, 0, -1, 0, -2, 2], 
            and target = 0.
    Output: [
                [-1,  0, 0, 1],
                [-2, -1, 1, 2],
                [-2,  0, 0, 2]
            ]


``` java
/*
 *Author: yeh
 *Time: 2017_07_10
 *Language: Java
 *
 */

public class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        if(nums.length < 4) return ret;//illegle
        Arrays.sort(nums);
        int left;
        int midl;
        int midr;
        int right;
        int sum;
        int size = nums.length;//the name "nums.length" too long
        List<Integer> solution = null;
        for(left=0; left<size-3; left++) {
            //first candidate too large, search finished
            if(nums[left]+nums[left+1]+nums[left+2]+nums[left+3] > target) break;
            //first candidate too small
            if(nums[left]+nums[size-1]+nums[size-2]+nums[size-3] < target) continue;
            //same number, continue to avoid same solution set
            if(left>0 && nums[left]==nums[left-1]) continue;
            for(midl=left+1; midl<nums.length-2; midl++) {
                if(nums[left]+nums[midl]+nums[midl+1]+nums[midl+2] > target) break;
                if(midl>left+1 && nums[midl]==nums[midl-1]) continue;
                midr = midl + 1;
                right = nums.length - 1;
                while(midr < right) {
                    sum = nums[left] + nums[midl] + nums[midr] + nums[right];
                    if(sum == target) {
                        //add the solution
                        solution = new ArrayList<Integer>();
                        solution.add(nums[left]);
                        solution.add(nums[midl]);
                        solution.add(nums[midr]);
                        solution.add(nums[right]);
                        ret.add(solution);
                        //get next num not equal this
                        while(midr<right && nums[midr]==nums[midr+1]) midr++;
                        while(right>midr && nums[right]==nums[right-1]) right--;
                        midr++;
                        right--;
                    }else if(sum < target) {
                        midr++;
                    }else{//sum > target
                        right--;
                    }
                }
            }
        }
        return ret;
    }
}


```
