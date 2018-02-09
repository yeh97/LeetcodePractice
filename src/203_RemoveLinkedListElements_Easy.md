


### Leetcode 203
#### [Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements)

  

##### ***Problem:***

	Remove all elements 
	from a linked list of integers that have value val.
	
##### ***Example:***

    Input: 1->2->1->3, 1
        Output: 2->3

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_09
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
    public ListNode removeElements(ListNode head, int val) {
        // 2018/2/9 : 2ms
        ListNode phead = new ListNode(0);
        ListNode pre = phead;
        phead.next = head;
        for (ListNode p = phead.next; p != null; p = p.next) {
            if (p.val != val) {
                pre = p; // p == pre.next
            } else {
                pre.next = p.next; // delete elem p
            }
        }
        return phead.next;
    }
}

```
