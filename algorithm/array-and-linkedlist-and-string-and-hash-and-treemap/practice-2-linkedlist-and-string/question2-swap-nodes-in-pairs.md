# Question2 Swap Nodes in Pairs

````java

/*
Clarification& Assumption:
    - input: head ListNode, single without random
    - output: head ListNode with swapPairs
High Level:
    - swap pair iteratively from the headNode

Middle Level:
    - iterated method:
        - iteratively find the next twoNode 
        - use prev, firstNode, secondNode, next to swap firstNode and secondNode
        - If only one left not needt to continue
    - recursive meethod: 
        - still use 4 indexs, prev, firstNode, seconcNode, 
        - swap the nextNode, and have the newHead
        - swap prev, firstNode, secondNode
        - return newHead
TC & SC: O(n), O(n)
 */

class Solution {
    public ListNode swapPairs(ListNode head) {
        // sanity check
        if (head == null || head.next == null) {
            return head;
        }
        //
        // ListNode iterHead = iterFind(head);
        ListNode recurHead = recurFind(head);
        return recurHead;
    }
    private ListNode recurFind(ListNode cur) {
        if (cur == null || cur.next == null) {
            return cur;
        }
        ListNode next = recurFind(cur.next.next);
        ListNode firstNode = cur;
        ListNode secondNode = cur.next;
        firstNode.next = next;
        secondNode.next = firstNode;
        return secondNode;
    }
    private ListNode iterFind(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode dummyNode = new ListNode(-1);
        dummyNode.next = head;
        ListNode prev = dummyNode;
        ListNode cur = head;
        while (cur != null && cur.next != null) {
            ListNode firstNode = cur;
            ListNode secondNode = cur.next;
            ListNode nextNode = cur.next.next;
            firstNode.next = nextNode;
            secondNode.next = firstNode;
            prev.next = secondNode;

            prev = firstNode;
            cur = nextNode;
        }
        return dummyNode.next;
    }
}
```
````
