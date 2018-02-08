### Leetcode 19
#### [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list)

    Given a linked list, 
    remove the n-th node from the end of list and return its head.

**Note:**

    Given n will always be valid.

    
**Example:**

    Input: 1->2->3->4->5, and n = 2.
    Output: 1->2->3->5. 
            (return head of the list)

> *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_10
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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if(head==null || n<0) return head;
        ListNode phead = null;
        ListNode first = head;
        ListNode second = head;
        for(int i=0; i<n; i++) {
            first = first==null ? null:first.next;
        }
        while(first != null) {
            phead = second;
            second = second==null ? null:second.next;
            first = first==null ? null:first.next;
        }
        if(phead == null) {
            head = second==null ? null:second.next;
        }else{
            phead.next = second==null ? null:second.next;
        }
        return head;
    }
}

```

> *Method #2*

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if(head==null || n<=0) return head;
        ListNode prehead = new ListNode(0);
        prehead.next = head;
        ListNode curnode = prehead;
        int length = getLength(head);
        for(int index=length-n; index>0; index--) {
            curnode = curnode.next;
        }
        curnode.next = curnode.next==null ? null:curnode.next.next;
        return prehead.next;
    }
    public static int getLength(ListNode head) {
        int length = 0;
        for(; head!=null; head=head.next) length++;
        return length;
    }
}

```
