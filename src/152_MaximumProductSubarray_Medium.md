

### Leetcode 152
#### [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray)

  

##### ***Problem:***

    Find the contiguous subarray within an array (containing at least one number) which has the largest product.
    
##### ***Example:***

    Input: [2,3,-2,4]
        Output: 6


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_01_29
 *Language: Java
 *
 */

class Solution {
    public int maxProduct(int[] nums) {
        // 2018/1/29 : 3ms
        if (nums == null || nums.length == 0) return 0;
        int curmaxv = nums[0], curminv = nums[0];
        int maxres = nums[0];
        for (int i = 1; i < nums.length; i++) {
            int tempmaxv = curmaxv, tempminv = curminv;
            // max(min)Product(nums[0...i]) : curmax(min)v
            curmaxv = Math.max(Math.max(nums[i], tempmaxv * nums[i]), tempminv * nums[i]);
            curminv = Math.min(Math.min(nums[i], tempmaxv * nums[i]), tempminv * nums[i]);
            maxres = Math.max(maxres, curmaxv);
        }
        return maxres;
    }
}

```
