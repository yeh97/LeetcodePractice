

### Leetcode 4
#### [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays)
  
    There are two sorted arrays nums1 and nums2 of size m and n respectively. 
    
    Find the median of the two sorted arrays.
    The overall run time complexity should be O(log (m+n)).

**examples:**
> * _nums1 = [2], nums2 = [], The median is 2.0_
> * _nums1 = [1, 3], nums2 = [2], The median is 2.0_
> * _nums1 = [1, 2], nums2 = [3, 4], The median is (2 + 3)/2 = 2.5_

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_05
 *Language: Java
 *
 */
 

public class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int length = nums1.length + nums2.length;
        if(length%2 == 1) {
            return (double)findKthSortedArrays(nums1, 0, nums1.length-1, 
                                       nums2, 0, nums2.length-1, length/2+1);
        }else{
            double l = (double)findKthSortedArrays(nums1, 0, nums1.length-1, 
                                           nums2, 0, nums2.length-1, length/2);
            double r = (double)findKthSortedArrays(nums1, 0, nums1.length-1, 
                                           nums2, 0, nums2.length-1, length/2+1);
            return (l+r)*0.5;
        }
    }
    //nums1 : [s1, e1]   nums2 : [s2, e2]
    public static int findKthSortedArrays(int[] nums1, int s1, int e1,
                          int[] nums2, int s2, int e2, int k) {
        int l1 = e1 - s1 + 1;
        int l2 = e2 - s2 + 1;
        if(l1 > l2) return findKthSortedArrays(nums2, s2, e2, nums1, s1, e1, k);
        if(l1 == 0) return nums2[k-1];
        if(k == 1) return Math.min(nums1[s1], nums2[s2]);
        int part1 = Math.min(l1, k/2);
        int part2 = k - part1;
        if(nums1[s1+part1-1] < nums2[s2+part2-1]) {
            //nums1 : [s1, s1+part1-1] must be lower by Kth
            return findKthSortedArrays(nums1, s1+part1, e1, nums2, s2, e2, k-part1);
        }else if(nums1[s1+part1-1] > nums2[s2+part2-1]) {
            //nums2 : [s2, s2+part2-1] must be lower by Kth
            return findKthSortedArrays(nums1, s1, e1, nums2, s2+part2, e2, k-part2);
        }else{
            //nums1[s1+part1-1] == nums2[s2+part2-1]
            //[s1, s1+part1-1].length + [s2, s2+part2-1].length = part1 + part2 = k
            return nums1[s1+part1-1];
        }
    }
}

```


