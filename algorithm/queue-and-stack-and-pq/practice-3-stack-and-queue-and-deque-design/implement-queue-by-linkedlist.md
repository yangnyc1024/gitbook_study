# Implement Queue by LinkedList

API(小心只有一个或者两个元素，head == null, head.next == null)

* poll(): poll from head
  * if head == null?
  * if head.next == null?
  * curNode = head && head = head.next && curNode.next = null && size--;
* peek():
* offer():offer from tail
  * if tail == null?
  * tail.next = curNode; & tail = tail.next; & size++



```java
public class Queue {
    private ListNode head;
    private ListNode tail;
    private int size;
    public Queue() {
        head = tail = null;
        size = 0;
    }
    public Integer poll() {
        if (head == nul) {
            return null;
        }
        if (head.next == null) {
            Integer result = head.next;
            head = tail = null;
            size--;
            return result;
        }     
        ListNode node = head;
        head = head.next;
        node.next = null;
        size--l
        return node.value; 
    }
    public Integer peek() {
        if (head == null) {
            return null;
        }
        return head.value;
    }
    public boolean offer(Integer ele) {
        if (head == null) {
            head = new ListNode(ele);
            tail = head;
        } else {
            ListNode cur = new ListNode(ele);
            tail.next = cur;
            tail = tail.next; // tail = cur;?
        }
        size++;
        return true;
    }
}
```
