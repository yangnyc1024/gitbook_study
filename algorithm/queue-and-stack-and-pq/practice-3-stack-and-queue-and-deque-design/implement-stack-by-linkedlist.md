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
        
    }

}// Some code
```















注意Integer和int的区别，后者不允许null的出现
