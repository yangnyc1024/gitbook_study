# Problem 8 Remove Linked List

![](<../../.gitbook/assets/Screenshot 2023-08-21 at 1.30.55 AM.png>)

```
// Some code
ListNode removeElemnts(ListNode head, int val) {
    ListNode dummy = new ListNode();
    dummy.next = head;
    prev.dummy;
    cur = head;
    while (cur != null) {
        if (cur.val == val) {
            prev.net = cur.next
        }
        else {
            prev = cur;
        }
        cur = cur.next;
    }
    return dummy.next;
}
```
