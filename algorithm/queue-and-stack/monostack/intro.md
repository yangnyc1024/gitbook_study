---
description: Intro
---

# Intro

## Summary

* 单调栈就是个stack, Mono Stack is a Stack
* 分类
  * 单调递增/单调递减
* use case
  * <mark style="color:red;">当你想知道谁谁右边/左边</mark>，<mark style="color:blue;">第一个</mark><mark style="color:red;">比它 大/小</mark>
  * 一段区间的最小/最大
* 原则上如何维护单调栈？
  * <mark style="color:blue;">来了个客人，破坏了单调性，不能让客人走，里面的数走</mark>
    * 谁挡住我进入，那就把它踢了
  * 新来的，无论如何都要进栈
  * <mark style="color:red;">被置换出栈的人已经完成了历史使命</mark>

## Details

### 经典Use Case: 找右边第一个比我小于的人& <mark style="color:orange;">单调非递减栈</mark>

* 相当于\[2,3,5,8] 来个4， 那就会变成\[2,3,4]

```java
while (!monoStack.isEmpty() && !monoStack.peekLast() > newElement) {
    monStack.pollLast();
}
monoStack.offerLast(newElement);
```

### 经典Use Case: 找右边第一个比我大于的人 & <mark style="color:green;">单调非递增栈</mark>

* 相当于\[8,5,3,2] 来个4， 那就会变成\[8,5,4]

```java
while (!monoStack.isEmpty() && !monoStack.peekLast() < newElement) {
    monStack.pollLast();
}
monoStack.offerLast(newElement);
```

### 经典Use Case: 找右边第一个比我小于等于的人  & <mark style="color:orange;">单调递减栈</mark>

* 相当于\[2,3,5,8] 来个3， 那就会变成\[2,3]

```java
while (!monoStack.isEmpty() && !monoStack.peekLast() >= newElement) {
    monStack.pollLast();
}
monoStack.offerLast(newElement);
```

### 经典Use Case: 找右边第一个比我大于等于的人& <mark style="color:green;">单调递增栈</mark>

* 相当于\[8,5,3,2] 来个3， 那就会变成\[8,5,3]

```java
while (!monoStack.isEmpty() && !monoStack.peekLast() <= newElement) {
    monStack.pollLast();
}
monoStack.offerLast(newElement);
```



### Example

* 上述的这些写法，栈内记录的是元素本身: value，有的时候，题目问的是与距离（distance）相关的问题
  * 你距离你右边/左边，第一个比你大/小的元素的距离是多少
  * 单调栈内有可能放的是元素的index

<mark style="color:blue;">求每个元素右边第一个比自己小的元素是谁，距离自己多远</mark>

* \[3,1,2,5,4,7,6], 单调递增栈\[1,2,4,6]
* result
  * 3: 1
  * 5: 4
  * 7: 6
  * 使得自己弹出来的那个元素就是第一个比自己小的

```java
// Some code

while (!monoStack.isEmpty() && array[curIndex] < array[monoStack.peekLast()]) {
    int 被我置换出来的元素index = monoStack.pollLast();
    result[被我置换出来的元素index] = array[curIndex];//谁把你置换出来，谁就是你的结果
    distance[被我置换出来的元素index] = curIndex - 被我置换出来的元素的index
}
```

### TC \&SC

* 每个元素只进出栈一次，每个元素出栈的时候，这个元素对应的solution就确定了
* 都是O(n)

