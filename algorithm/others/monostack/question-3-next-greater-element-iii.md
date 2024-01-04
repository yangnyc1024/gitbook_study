# Question 3 Next Greater Element III

* 找右边第二个比你大的

### Analysis

* 我们已经知道，常规的use case: next greater element 可以用单调栈实现O(n)的解法
* 原来只有一类的元素：栈内等待右边第一个比我大的元素==> 普通单调栈
* 现在又多了一类元素：它已经被第一个比他的的人置换出来，但是第二个人还没有来==> 又是一个单调栈

### Details

* stack 1(还在等待第一次被置换的人)
* stack 2(还在等待第二次被置换的人)
* temp stack（为了保持stack 2里面的和stack 1里面的顺序，所以需要用一个来倒腾）
  * 当有元素被stack 1里面替换出来放进stack2的时候，需要用temp stack倒腾一下
* example&#x20;
  * \[10, 2,3,4, 0, 9,6]
  * stack 1: 10，4
  * stack 2: 3
  * result: 2: 4



```java
// Some code

public int secondGreaterElement(int[] array) {
    int[] result = new int[array.length];
    Arrays.fill(result, -1);
    Dequeue<Integer> stack1 = new ArrayDeque<>();
    Dequeue<Integer> stack2 = new ArrayDeque<>();
    Dequeue<Integer> temp = new ArrayDeque<>();
    for (int i = 0; i < array.length; i++) {
        while (!stack2.isEmpty() && array[stack2.peekLast()] < array[i]) {
            result[stack2.pollLast()] = array[i];
        }
        while (!stack1.isEmpty() && array[stack.peekLast()] < array[i]) {
            stack2.offerLast(temp.pollLast());
        }
        stack1.offerLast(array[i]);
    }
    return result;
}
```
