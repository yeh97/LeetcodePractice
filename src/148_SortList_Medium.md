

### Leetcode 148
#### [Sort List](https://leetcode.com/problems/sort-list)

  

##### ***Problem:***

    Sort a linked list in O(n log n) time using constant space complexity.

    
##### ***Example:***

    Input: [1,2,4,3]
        Output: [1,2,3,4]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_01_28
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
class Solution {
    public ListNode sortList(ListNode head) {
        // 2018/1/28 : 284ms
        qsort(head);
        return head;
    }
    // linkedlist quick sort
    public static void qsort(ListNode head) {
        qsort(head, null);
    }
    // private function :
    private static void qsort(ListNode head, ListNode tail) {
        if (head == null || head == tail) return;
        ListNode p = qsortPartion(head, tail);
        qsort(head, p);
        qsort(p.next, tail);
    }
    private static ListNode qsortPartion(ListNode head, ListNode tail) {
        // if (head == null || head == tail) return head;
        int key = head.val;
        ListNode p = head;
        for (ListNode q = head.next; q != tail; q = q.next) {
            if (q.val < key) {
                p = p.next;
                swapVal(p, q);
            }
        }
        swapVal(p, head);
        return p;
    }
    private static void swapVal(ListNode p, ListNode q) {
        int val = p.val;
        p.val = q.val;
        q.val = val;
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2018_01_28
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
class Solution {
    public ListNode sortList(ListNode head) {
        // 2018/1/28 : 7ms
        return mergesort(head);
    }
    // Merge Sort
    public ListNode mergesort(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode mid = cutList(head);
        ListNode behind = mergesort(mid);
        ListNode front = mergesort(head);
        // merge two sorted lists
        return mergeList(behind, front);
    }
    private ListNode cutList(ListNode head) {
        if (head == null || head.next == null) return null;
        // node(low) is the medium of the list
        ListNode low = head;
        ListNode fast = head;
        ListNode prelow = null;
        while (fast != null && fast.next != null) {
            prelow = low;
            low = low.next;
            fast = fast.next.next;
        }
        // cut list
        prelow.next = null;
        return low;
    }
    private ListNode mergeList(ListNode L1, ListNode L2) {
        ListNode phead = new ListNode(0);
        ListNode cur = phead;
        while (L1 != null && L2 != null) {
            if (L1.val < L2.val) {
                cur = cur.next = L1;
                L1 = L1.next;
            } else {
                cur = cur.next = L2;
                L2 = L2.next;
            }
        }
        cur.next = L1 != null ? L1 : L2;
        return phead.next;
    }
}

```

