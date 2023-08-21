# Problem 5 Add Two Numbers



```java
ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode next = null;
    while (head != null) {
        next = head.next;
        // prev, head, next按照顺序排好
        head.next = prev;
        prev = head;
        head = next;
    }
    return prev;
}
```
