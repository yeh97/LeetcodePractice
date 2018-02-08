

### Leetcode 138
#### [Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer)

  

##### ***Problem:***

    A linked list is given such that each node     
    contains an additional random pointer 
    which could point to any node in the list or null.

    Return a deep copy of the list.

    
##### ***Example:***

    Input: [null]
        Output: [null]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_26
 *Language: Java
 *
 */

/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) return null;
        // copy node to newNode, node -> newNode -> next
        for (RandomListNode node = head; node != null; node = node.next.next) {
            RandomListNode newNode = new RandomListNode(node.label);
            newNode.next = node.next;
            node.next = newNode;
        }
        // copy random
        for (RandomListNode node = head; node != null; node = node.next.next) {
            if (node.random == null) continue;
            // node.next : newNode
            node.next.random = node.random.next;
        }
        // separate out new list
        RandomListNode newHead = head.next;
        RandomListNode node = head;
        RandomListNode newNode = null;
        while (true) {
            newNode = node.next;
            node = node.next = newNode.next;
            if (node == null) break;
            newNode.next = newNode.next.next;
        }
        return newHead;
    }
}


```


