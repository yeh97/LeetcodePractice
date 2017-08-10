

### Leetcode 92
#### [Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii)

  

##### ***Problem:***

    Reverse a linked list from position m to n. 
    Do it in-place and in one-pass.
    Given m, n satisfy the following condition : 1 <= m, n <= length of list.
    

##### ***Example:***

    Input: 1->2->3->null, 2, 3
        Output: 1->3->2->null

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_10
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
    public ListNode reverseBetween(ListNode head, int m, int n) {
        // assert (1 <= m, n <= Length(head))
        if (m <= 0 || n <= 0) return head;
        if (m > n) return reverseBetween(head, n, m);
        if (m == n) return head;
        //reverse from m to n
        ListNode phead = new ListNode(0);
        phead.next = head;
        ListNode rs = nextKNode(phead, m - 1);
        rs.next = reverseKNode(rs.next, n - m + 1);
        return phead.next;
    }
    private ListNode nextKNode(ListNode head, int k) {
        for (int i = 0; head != null && i < k; i++) {
            head = head.next;
        }
        return head;
    }
    private ListNode reverseKNode(ListNode head, int k) {
        if (head == null) return null;
        ListNode cur = head;
        ListNode pre = null;
        ListNode t = null;
        for (int i = 0; cur != null && i < k; i++) {
            t = cur.next;
            cur.next = pre;
            pre = cur;
            cur = t;
        }
        head.next = cur;
        return pre;
    }
}
```


