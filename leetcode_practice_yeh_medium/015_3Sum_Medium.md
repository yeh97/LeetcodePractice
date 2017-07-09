

### Leetcode 15
#### [3Sum](https://leetcode.com/problems/3sum)

    Given an array S of n integers, 
    are there elements a, b, c in S such that a + b + c = 0? 
    Find all unique triplets in the array which gives the sum of zero.

**Note:**

    The solution set must not contain duplicate triplets.
    
**Example:**

    Input S = [-1, 0, 1, 2, -1, -4],
    Ouput : [[-1, 0, 1], [-1, -1, 2]]

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_09
 *Language: Java
 *
 */

public class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        if(nums==null || nums.length==0) return ret;
        Arrays.sort(nums);
        //record the sum of set
        //in this function, the target is 0
        int target;
        //the index of three number in the solution set
        int left;
        int mid;
        int right;
        //the solution set
        List<Integer> sol = null;
        for(left=0; left<nums.length; left++) {
            //nums[left] is the smallest number in set
            //if nums[left] > 0, the sum of set > 0
            if(nums[left] > 0) break;
            //avoid set repeat
            if(left>0 && nums[left]==nums[left-1]) continue;
            //get mid, right
            mid = left + 1;
            right = nums.length - 1;
            while(right > mid) {
                target = nums[left] + nums[mid] + nums[right];
                if(target == 0) {
                    //nums[left], nums[mid], nums[right] is a solution set
                    sol = new ArrayList<Integer>();
                    sol.add(nums[left]);
                    sol.add(nums[mid]);
                    sol.add(nums[right]);
                    ret.add(sol);
                    //avoid set repeat
                    //get next num not equal with this num
                    while(mid<right && nums[mid]==nums[mid+1]) mid++;
                    while(right>mid && nums[right]==nums[right-1]) right--;
                    mid++;
                    right--;
                }else if(target < 0) {
                    //the sum too small
                    mid++;
                }else{//target > 0
                    right--;
                }
            }
        }
        return ret;
    }
}


```
