# Implement Stack by LinkedList

stack的api

* push
  *
* pop
* peek
* isEmpty
* size



需要注意的是，哪个是stack顶？

* if it is the head?
  * push, O(1)
  * pop, O(1)
* if it is the tail?
  * push, O(n)
  * pop, O(n)



```java
public class Stack {
    private ListNode head;
    private int size;
    public Stack() {
        this.head = null;
        this.size = 0;
    }
    public Integer pop() {
        if (head == null) {
            return null;
        }
        ListNode result = head;
        head = head.next;
        result.next = null;
        return result.value;
    }
    public Integer peek() {
        if (head == null) {
            return null;
        }
        return head.value;
    }
    
    public boolean push(int element) {
        ListNode newNode = new ListNode(element);
        newNode.next = head;
        head = newNode;
        size++;
        return true;
    }
    public int size() {
        return size;
    }
    public boolean isEmepty() {
        return size == 0;
    }
}
```















注意Integer和int的区别，后者不允许null的出现
