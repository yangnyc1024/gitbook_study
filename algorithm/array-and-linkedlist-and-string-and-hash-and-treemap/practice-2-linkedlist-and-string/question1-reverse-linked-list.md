# Question1 Reverse Linked List



````java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */

 /*
Clarification/ Asssumption: 
    - input: a given listNode, 
    - output: a listNode have been reverseList
    - regular linkedlist(no circular, no double), with int val
High Level:
    - iterately reverse each linkedlist start from the head until to the last one(which next is null) one by one
    - recursively reverse each linkedlist by use the same recrusively function

Middle Level:
    - iterate: each time, 
        - find nextNode
        - reverse curNode by curNode.next = prev
        - dont forget move cur index to nextNode , prev index to curNode
    - recursive function
        - function: given a listNode head, return a revserive listNode head
        - base case: ony one listNode
        - subproblem: k -1 listNode, or cur.next problem
        - recursive rule:
            - cur.next.next = cur, cur.next = null;
            - return head
TC & SC: O(n), O(1)
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        // corner case
        if (head == null || head.next == null) {
            return head;
        }
        //
        ListNode newHeadIter = revIter(head);
        // ListNode newHeadRecur = revRecur(head);
        return newHeadIter;
        // return newHeadRecur;  
    }
    private ListNode revIter(ListNode cur) {
        ListNode prev = null;
        while (cur != null) {
            ListNode next = cur.next;
            cur.next = prev;
            // cur = next;!!!
            prev = cur;
            cur = next;
        }
        return prev; 
    }
    private ListNode revRecur(ListNode cur) {
        if (cur.next == null) {
            return cur;
        }
        ListNode newHead = revRecur(cur.next);
        cur.next.next = cur;
        cur.next = null;
        return newHead;
    }
}
```
````
