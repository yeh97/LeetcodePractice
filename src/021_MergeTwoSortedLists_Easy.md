### Leetcode 21
#### [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists)

    Merge two sorted linked lists and 
    return it as a new list. 
    
    The new list should be made by splicing
    together the nodes of the first two lists.
 
 ***Example:***
 
    Input: [1,4,6]  [2,3,7,10]
    Ouput: [1,2,3,4,7,10] 
            (return the head)
    

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_11
 *Language: Java
 *
 */

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode phead = new ListNode(0);
        ListNode pre = phead;
        while(l1!=null && l2!=null) {
            if(l1.val < l2.val) {
                pre.next = l1;
                l1 = l1.next;
            }else{
                pre.next = l2;
                l2 = l2.next;
            }
            pre = pre.next;
        }
        //(l1==null || l2==null) == true
        //if(l1!=null) l2==null
        //-> pre.next = l1;
        pre.next = l1==null ? l2:l1;
        return phead.next;
    }
}


```
