

### Leetcode 86
#### [Partition List](https://leetcode.com/problems/partition-list)

  

##### ***Problem:***

    Given a linked list and a value x, 
    partition it such that all nodes less than x come before nodes greater than or equal to x.

    You should preserve the original relative order of the nodes in each of the two partitions.

##### ***Example:***

    Input: [1,4,3,2,5,2], 3
        Output: [1,2,2,4,3,5]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_09
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
    public ListNode partition(ListNode head, int x) {
        //if (head == null) return null;
        ListNode preNotLess = new ListNode(0);
        ListNode preLess = new ListNode(0);
        ListNode prenl = preNotLess;
        ListNode prel = preLess;
        for (ListNode cur = head; cur != null; cur = cur.next) {
            if (cur.val < x) {
                prel = prel.next = cur;
            } else {
                prenl = prenl.next = cur;
            }
        }
        prenl.next = null;
        prel.next = preNotLess.next;
        return preLess.next;
    }
}
```


