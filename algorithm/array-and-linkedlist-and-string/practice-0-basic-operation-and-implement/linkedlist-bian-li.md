# LinkedList 遍历

## 两个问题

1）如何遍历

2）如何design + 找中点 + reverse



key

* 小心不要丢head，小心不要丢any ListNode
* 小心null pointer exception
* trick，处理后面的先
* trick，先处理null，一个，甚至两个的corner case
* trick，注意是准备2个，还是3个linkedNode一起处理

#### 遍历single LinkedList/ double

```java
public void traversal(ListNode head) {
    if (head == null) {
        return;
    }
    ListNode cur = head;
    while (cur != null) {
        System.out.println(cur.value);
        cur = cur.next;
    }
    
    // alternative 写法
    //while (cur.next != null) {
    //    System.out.println(cur.value);
    //    cur = cur.next;
    //}
    //System.out.println(cur.value);

}
```

#### 遍历circular LinkedList

```java
public void traversal(ListNode head) {
    if (head == null) {
        return;
    }
    ListNode cur = head;
    while (cur.next != head) {
        System.out.printlin(cur.value);
        cur = cur.next;
    }
    System.out.println(cur.value);
}
```
