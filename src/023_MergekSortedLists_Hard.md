

### Leetcode 23
#### [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists)

    Merge k sorted linked lists and 
    return it as one sorted list. 
    
    Analyze and describe its complexity.

##### *Method #1*
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
    
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists==null || lists.length==0) return null;
        ListNode phead = new ListNode(0);
        ListNode pre = phead;
        //sorted from small to big number
        Comparator<ListNode> cmp = new Comparator<ListNode>() {
            public int compare(ListNode a, ListNode b) {
                //assert(a!=null && b!=null)
                if(a.val < b.val) return -1;
                else if(a.val > b.val) return 1;
                else return 0;//a.val == b.val
            }
        };
        //Heap sort
        Queue<ListNode> q = new PriorityQueue<>(lists.length, cmp);
        for(ListNode p : lists) {
            if(p != null) q.add(p);
        }
        while(!q.isEmpty()) {
            pre.next = q.poll();
            pre = pre.next;
            if(pre.next != null) q.add(pre.next);
        }
        return phead.next;
    }
}

```

##### *Method #2*
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
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists==null || lists.length==0) return null;
        if(lists.length == 1) return lists[0];
        ListNode[] next = null;
        //similar with merge sort
        while(lists.length > 1) {
            next = new ListNode[(lists.length+1)>>1];
            for(int i=0; i<next.length-1; i++) {
                next[i] = mergeTwoLists(lists[i<<1], lists[i<<1|1]);
            }
            if((lists.length&1) == 1) {
                next[next.length-1] = lists[lists.length-1];
            }else{
                next[next.length-1] = mergeTwoLists
                    (lists[lists.length-1], lists[lists.length-2]);
            }
            lists = next;
        }
        return lists[0];
    }
    public static ListNode mergeTwoLists(ListNode l1, ListNode l2) {
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
        pre.next = l1==null ? l2:l1;
        return phead.next;
    }
}
```
