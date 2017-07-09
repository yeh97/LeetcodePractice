

### Leetcode 1
#### [Two Sum](https://leetcode.com/problems/two-sum)
  
    Given an array of integers, 
    return indices of the two numbers 
    such that they add up to a specific target. 
    You may assume that 
    each input would have exactly one solution, 
    and you may not use the same element twice.

**examples:**

    Given nums = [2, 7, 11, 15], target = 9,
    Because nums[0] + nums[1] = 2 + 7 = 9,
    return [0, 1].

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_04
 *Language: Java
 *
 */

public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] ret = new int[2];
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for(int i=0; i<nums.length; i++) {
            if(map.containsKey(nums[i])) {
                ret[0] = map.get(nums[i]);
                ret[1] = i;
                return ret;
            }else{
                map.put(target - nums[i], i);
            }
        }
        return ret;
    }
}

```
