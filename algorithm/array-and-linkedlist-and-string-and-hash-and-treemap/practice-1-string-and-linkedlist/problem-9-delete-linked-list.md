# Problem 9 Delete Linked List

```java
public void deleteNode(ListNode node) {
    node.val = node.nexxt.val;
    node.next = node.next.next;
}
```
