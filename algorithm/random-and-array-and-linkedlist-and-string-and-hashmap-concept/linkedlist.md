# LinkedList

## 两个问题

1）如何遍历

2）如何design

* addHead/addTail
* addIndex
* deleteHead/deleteTail
* find
*



### Single LinkedList









### Double LinkedList

```java




public void addHead(int val) {
    ListNode newNode = new ListNode(val);
    if (head == null) {
        head = newNode;
        tail = newNode;
    }
    else {
        newNode.next = head;
        head.prev = newNode;
        head = newNode;
    }
    size++;
}
```



