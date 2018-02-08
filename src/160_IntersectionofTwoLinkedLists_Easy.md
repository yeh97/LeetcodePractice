

### Leetcode 160
#### [Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists)

  

##### ***Problem:***

    Write a program to find the node at which the intersection of two singly linked lists begins.
    
##### ***Example:***

    Input: [1],[2]
        Output: null

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_01_30
 *Language: Java
 *
 */

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        // 2018/1/30 : 2ms
        if (headA == null || headB == null) return null;
        int la = getLength(headA);
        int lb = getLength(headB);
        ListNode ta = nextKNode(headA, la - lb);
        ListNode tb = nextKNode(headB, lb - la);
        // getLength(ta) == getLength(tb)
        while (ta != null && ta != tb) {
            ta = ta.next;
            tb = tb.next;
        }
        return ta;
    }
    public int getLength(ListNode head) {
        int ret = 0;
        for (; head != null; head = head.next) ret++;
        return ret;
    }
    public ListNode nextKNode(ListNode head, int t) {
        for (int i = 0; i < t && head != null; i++) head = head.next;
        return head;
    }
}

```

