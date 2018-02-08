

### Leetcode 31
#### [Next Permutation](https://leetcode.com/problems/next-permutation)

    Implement next permutation, 
    which rearranges numbers into the lexicographically 
    next greater permutation of numbers.

    If such arrangement is not possible, 
    it must rearrange it as the lowest possible order 
    (ie, sorted in ascending order).

    The replacement must be in-place, 
    do not allocate extra memory.

    
***Example:***

    Input: 1, 2, 3
        Ouput: 1, 3, 2
    Input: 3, 2, 1
        Ouput: 1, 2, 3
    Input: 1, 1, 5
        Ouput: 1, 5, 1

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_16
 *Language: Java
 *
 */

public class Solution {
    public void nextPermutation(int[] nums) {
        if(nums==null || nums.length<2) return;
        //case #1: permutation of nums is max, return reverse
        //case #2: exits index, nums[index]<nums[index+1], or it's max
        //a[n]<=a[n-1]<=..a[i], a[i]<a[i+1], the permutation of a[i+1]...a[n] is max 
        //get the smallest in a[j] when a[j]>=a[i] && j>i
        //the next permutation: i) swap a[i], a[j]; ii) reverse a[i+1]...a[n]
        int i = nums.length - 2;
        while(i>=0 && nums[i]>=nums[i+1]) {
            i--;
        }
        if(i >= 0) {
            /*Method #1
            int j = nums.length - 1;
            while(nums[j] <= nums[i]) {
                j--;
            }
            */
            //Method #2
            int j = i + 1;
            while(j<nums.length && nums[j]>nums[i]) {
                j++;
            }
            j--;
            swap(nums, i, j);
        }
        reverse(nums, i+1, nums.length);
    }
    private static void swap(int[] nums, int i, int j) {
        int t = nums[i];
        nums[i] = nums[j];
        nums[j] = t;
    }
    private static void reverse(int[] nums, int start, int end) {
        int l = start;
        int r = end - 1;
        while(l < r) {
            swap(nums, l, r);
            l++;
            r--;
        }
    }
}


```
