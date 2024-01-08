# Subtopic: 谁小移谁

always move the smallest point



## Question 1: Marge 2 sorted array, Merge k sorted array/LinkedList



问题1:如何在k个poiner中找到最小的一个？minHeap

问题2:minHeap里面存什么？

* PriorityQueue\<Pair<是哪个list，list中的index，value>>





## Question 4 Given two sorted arrays, get the intersection/union/difference.&#x20;

Assumption: there are no duplicate elements in each of the arrays



```java
// 谁小移谁

if (A[i] < B[j]) {
    // union.add(A[i]);
    // diff.add(A[i]);
    i++;
} else if (A[i] > B[j]) {
    // union.add(B[i]);
    // diff.add(B[i]);
    j++;
}
else { //相同
    // intersection.add(A[i]);
    // union.add(B[i]);
    i++;
    j++;
}


//post processing
while (i < lenA) {  //j >= len B
    union.add(arrayA[i]);
    diff.add(arrayA[i]);
    i++;
}

while (j < lenB) {  //i >= len A
    union.add(arrayB[j]);
    diff.add(arrayB[j]);
    j++;
}
```

TC & SC: O(n), O(1)



#### 以intersection为例证明谁小移谁

* 证明求出来的intersection是正确的？
* Bruce force:
  * for each B\[j]: 有没有一个A\[i] == B\[j]?
* 有的话，那就加入
* 如果没有的话
  * 那么左边右边，应该没有
  * 所以A中没有的话，那就可以j++说明她不是

### Question 4.1 how about duplicates in the arrays



## Question 5.0 Three sorted arrays A， B， and C from each of the arrays pick one element, x from A, y form B, z from C, what is the minimum |x-y| + |y- z| + |z- x|

* 看到绝对值，不顺眼，就干掉他。。。
* use the order trick



考虑1为最小值的所有tuple





## Question 5.1 What about we have k sorted arrays we would like to pick one element from each of them, what is the smallest ranget = (max - min)

* merge k pointer using a size k minHeap
* how do we know the maximum value of the minHeap?
