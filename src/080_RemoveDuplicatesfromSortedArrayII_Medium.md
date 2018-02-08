

### Leetcode 80
#### [Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii)

  

##### ***Problem:***

    Follow up for "Remove Duplicates":
    What if duplicates are allowed at most twice?
    return new length, array also should be changed.

##### ***Example:***

    Input: [1,1,1,2,2,3]
        Output: 5 ([1,1,2,2,3])

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_08
 *Language: Java
 *
 */

public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int ret = 0;
        int next = 0;
        int index = 0;
        while (index < nums.length) {
            //search min of next : nums[next] != nums[index]
            //--> nums[i] == ... == nums[next - 1] != nums[next]
            //--> time of nums[i] == next - i
            next = index + 1;
            while (next < nums.length && nums[next] == nums[index]) {
                next++;
            }
            if (next - index > 1) {
                swap(nums, ret, index);
                swap(nums, ret + 1, index + 1);
                ret += 2;
            } else {
                swap(nums, ret, index);
                ret += 1;
            }
            index = next;
        }
        return ret;
    }
    private void swap(int[] nums, int i, int j) {
        int t = nums[i];
        nums[i] = nums[j];
        nums[j] = t;
    }
}

```


