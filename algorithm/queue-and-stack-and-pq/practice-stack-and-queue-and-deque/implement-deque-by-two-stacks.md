# Implement Deque by Two Stacks

#### Deque: Double End Queue:  first] \[ end

* Stack FILO本身具有的api
  * push(element)
  * pop()
  * peek()
  * isEmpty()
  * size()
* Deque需要的API:
  * offerFirst()
  * offerLast()
  * poll/peekFirst()
  * poll/peekLast()



#### 分析

两个stack背靠背放置的时候，把元素从右边倒腾到左边，元素顺序不变

* offerFirst: push in stack 1
* offerLast: push in stack2
* pollLast:&#x20;
  * S2里面如果有，S2里的最后一个O(1)
  * S2里面如果没有，transfer elements from S1 first + pop
* pollFirst:&#x20;
  * S1里面如果有，S1里的最后一个O(1)
  * S2里面如果没有，transfer elements from S2 first + pop
* size: => stack1.size() + stack2.size()
* isEmpty(): =>stack1.isEmpty() +stack2.isEmpty()

```java
class Solution {
    Deque<Integer> stack1;
    Deque<Integer> stack2;
    public Solution() {
        stack1 = new ArrayDeque<>();
        stack2 = new ArrayDeque<>();
    }
    public void offerLast(int element) {
    
    }
    
    public void offerFirst(int element) {
    
    }
    
    public Integer pollLast() {
    
    }
    public Integer peekLast() {
    
    }
    public Integer peekFirst() {
    
    }
    public int size() {
    
    }
    
    public void isEmpty() {
    
    }
    
    private void move(Deque<Integer> stackFrom, Deque<Integer> stackTo) {
    
    } 
}
```
