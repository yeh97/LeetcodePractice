

### Leetcode 2
#### [Add Two Numbers](https://leetcode.com/problems/add-two-numbers)
  
    You are given two non-empty linked lists 
    representing two non-negative integers. 
    
    The digits are stored in reverse order and 
    each of their nodes contain a single digit. 
    
    Add the two numbers and return it as a linked list.

    You may assume the two numbers do not contain any leading zero, 
    except the number 0 itself.

**examples:**

    Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
    Output: 7 -> 0 -> 8

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_04
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(0);
        ListNode ph = head;
        int carry = 0;
        int l1num;
        int l2num;
        while(l1!=null || l2!=null) {
            l1num = l1==null ? 0:l1.val;
            l2num = l2==null ? 0:l2.val;
            ph.next = new ListNode((l1num + l2num + carry) % 10);
            ph = ph.next;
            carry = (l1num + l2num + carry) / 10;
            l1 = l1==null ? null:l1.next;
            l2 = l2==null ? null:l2.next;
        }
        if(carry != 0) ph.next = new ListNode(carry);
        return head.next;
    }
}

```
