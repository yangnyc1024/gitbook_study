# Implement Deque by Three Stacks

关键步骤

* 当stack没有的时候，是从另一个stack倒腾一半过来
* 怎么倒腾？
  * 先把一半放在buffer里面
  * 剩下一半放到另外一边
  * 最后讲buffer放回到source里面



```java
public class Solution {
    private Deque<Integer> left;
    private Deque<Integer> right;
    private Deque<Integer> buffer;
    
    public DequeByThreeStacks() {
        left = new ArrayDeque<>();
        right = new ArrayDeque<>();
        buffer = new ArrayDeque<>();
    }
    public void offerFirst(int element) {
        left.offerFirst(element);
    }
    public void offerLast(int element) {
        right.offerFirst(element);
    }
    
    public void pollFirst() {
        if (left.isEmpty()) {
            move(right, left);
        }
        left.pollFirst();
    }
    
    public void peekFirst() {
        if (left.isEmpty()) {
            move(right, left);
        }
        left.peekFirst();
    }
    
    public void pollLast() {
        if (right.isEmpty()) {
            move(left, right);
        }
        right.pollFirst();
    }
    
    public void peekLast() {
        if (right.isEmpty()) {
            move(left, right);
        }
        right.peekFirst();
    }
    
    public int size() {
        return left.size() + right.size();
    }
    
    public boolean isEmpty() {
        return left.isEmpty() && right.isEmpty();
    }
    
    // when the destination stack is empty, move half of the elements form 
    // the source stack to the destination stack
    
    private void move (Deque<Integer> src, Deque<Integer> dest) {
        if (!dest.isEmpty()) {
            return;
        }
        int halfSize = src.size() / 2;
        // move src half to buffer
        for (int i = 0; i < halfSize; i++) {
            buffer.offerFirst(src.pollFirst());
        }
        // move rest src half to dest
        while (!src.isEmpty()) {
            dest.offerFirst(src.pollFirst());
        }
        // move buffer back to src
        while (!buffer.isEmpty()) {
            src.offerFirst(buffer.pollFirst());
        }
    }
}
```
