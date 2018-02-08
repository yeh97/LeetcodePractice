

### Leetcode 25
#### [Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group)

  

##### ***Problem:***

    Given a linked list, 
    reverse the nodes of a linked list k at a time
    and return its modified list.
    
    k is a positive integer and 
    is less than or equal to the length of the linked list. 
    
    If the number of nodes is not a multiple of k 
    then left-out nodes in the end should remain as it is.
    
    You may not alter the values in the nodes, 
    only nodes itself may be changed.
    
    Only constant memory is allowed.

##### ***Example:***

    Input: 1->2->3->4->5, 2
        Output: 2->1->4->3->5
    Input: 1->2->3->4->5, 2
        Output: 3->2->1->4->5

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_12
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
    public ListNode reverseKGroup(ListNode head, int k) {
        if(head==null || k<2) return head;
        ListNode phead = new ListNode(0);
        ListNode pre = phead;
        pre.next = head;
        for(int length=getLengthOfList(head); length>=k; length-=k) {
            head.next = reverseListKNode(pre, head, k);
            pre = head;
            head = head.next;
        }
        return phead.next;
    }
    private int getLengthOfList(ListNode head) {
        int length = 0;
        for(; head!=null; head=head.next) length++;
        return length;
    }
    //reverseListKNode return the next K node from head
    //make pre.next = the new head of the K node
    private ListNode reverseListKNode(ListNode pre, ListNode head, int k) {
        //assert(pre!=null && k>=2 && getLengthOfList(head)>=k)
        ListNode preHead = null;
        ListNode curNode = null;
        for(int i=0; i<k; i++) {
            preHead = head.next;
            head.next = curNode;
            curNode = head;
            head = preHead;
        }
        pre.next = curNode;
        return head;
    }
}


```
