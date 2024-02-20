# Implement Stack by Array

```java
public class Stack {
    private int[] array;
    private int head;
    public Stack(int cap) {
        array = new int[cap];
        head = array.length;
    }
    public boolean push(int ele){
        if (head == -1) return fasle;
        head--;
        array[head] = ele;
        return true;
    }
    public Integer pop() {
        if (head = array.length) {
            return null;
        }
        int curValue = array[head];
        head--;
        return curValue;
    }
    public Integer top() {
        if (head = array.length) {
            return null;
        }
        int curValue = array[head];
        return curValue;
    }
    public int size() {
        return array.length - head;
    }
    public int isEmpty() {
        return size() == 0;
    }
    public int isFull() {
        return size() == array.length;
    }
}
```
