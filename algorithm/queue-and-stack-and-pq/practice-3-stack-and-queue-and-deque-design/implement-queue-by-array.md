---
description: https://leetcode.com/problems/design-bounded-blocking-queue/
---

# Implement Queue by Array



High Level/思考方向：

*

细节：

* //这种方法记录的，相当于，有个head,有个tail，再有个size，我自然知道整个queue在哪里
* //另一种记录方式，相当于，有个head,有个tail，不需要给size，但是一直差一个1，我自然知道整个queue在哪里
* 这种只使用用bounded queue
* 头尾指针要注意移动，





注意：

* 这其实是个双指针
* head只能往右移动（因为<mark style="color:red;">head的右边是queue的第一个元素</mark>，head只是控制poll），tail只能往右移动（因为<mark style="color:red;">tail是queue的最后一个元素</mark>，tail它只控制opffer）
  * 注意我们这里用的是左开，右闭，
  * 长度(tail -head -1) % array.length，（head，tail],&#x20;
  * offer的话，(head, tail+1]
  * poll的话，(head + 1, tail]
  * peak的话，(head +1) % array.length
* 如果head的右边是tail，tail的左边是head，说明是empty
* 如果head==tail，说明是full



```java
package QueueStackDeque;


import java.util.*;


public class QueueByArrays2 {


   private int head; //private means the variable is only accessible inside the class
       // head is the head
   private int tail;
   private int[] array;
   //这种方法记录的，相当于，有个head,有个tail，再有个size，我自然知道整个queue在哪里
   //另一种记录方式，相当于，有个head,有个tail，不需要给size，但是一直差一个1，我自然知道整个queue在哪里


   public QueueByArrays2(int cap) {
       array = new int[cap + 1];
       head = 0;
       tail = 1;
   }


   public boolean offer(int ele) {
       if (isFull()) {
           return false;
       }
       array[tail] = ele;
       tail = tail + 1 == array.length ? 0: tail + 1;


       return true;


   }
   public Integer peek() {
       if (isEmpty()) {
           return null;
       }
       return array[(head + 1) % array.length];
   }


   public Integer poll() {
       if (isEmpty()) {
           return null;
       }
       int ret = array[head];
       head = (head + 1) % array.length;
       return ret;
   }


   public int size() {
       int size = tail - head - 1;
       return size % array.length; //???
       // return size < 0 ? array.length + size : size;
   }


   public boolean isEmpty() {
       return (head + 1) % array.length == tail; //???
   }


   public boolean isFull() {
       return head == tail; //???
   }




   public static void main(String[] args) {
       QueueByArrays2 q = new QueueByArrays2(3);
       q.offer(1);
       q.offer(2);
       q.offer(3);
       Integer ret = q.poll();
       System.out.println(ret);
       ret = q.poll();
       ret = q.poll();
       System.out.println(ret);
       q.offer(4);
       System.out.println(q.head);
       System.out.println(q.tail);
   }
}

```
