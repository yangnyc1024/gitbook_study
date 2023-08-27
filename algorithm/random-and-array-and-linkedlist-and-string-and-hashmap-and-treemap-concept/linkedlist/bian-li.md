# 遍历

遍历single LinkedList/ double

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

遍历circular LinkedList

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
