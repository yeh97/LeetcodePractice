

### Leetcode 147
#### [Insertion Sort List](https://leetcode.com/problems/insertion-sort-list)

  

##### ***Problem:***

    Sort a linked list using insertion sort.

    
##### ***Example:***

    Input: [1,2,4,3]
        Output: [1,2,3,4]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_01_27
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
    public ListNode insertionSortList(ListNode head) {
        // Binary Insertion Sort
        if (head == null || head.next == null) return head;
        // cut the list by the medium node
        ListNode mid = cutList(head);
        // insertionSort two lists
        ListNode behind = insertionSortList(mid);
        ListNode front = insertionSortList(head);
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

