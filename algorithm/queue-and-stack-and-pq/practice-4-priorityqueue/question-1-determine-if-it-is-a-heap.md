# Question 1 Determine if it is a heap

minHeap could be implemented by array;

用array实现的heap有什么特点：从index

* 当前的index是i:
  * 左边的孩子是2\* i + 1
  * 右边的孩子是2\* i + 2
* 堆序性
  * 每个subtree最值都在顶端
  * array\[i] < array\[2 \* i + 1], array\[i] < array\[2 \* i + 2]



```java
public boolean isMinHeap(int[] array) {
    // assume array is valid
    for (int i = 0 ; i < array.length; i++) {
        int currentValue = array[i];
        if (2 * i + 1 < array.length) {
            if (currentValue > array[2 * i + 1]) {
                return false;
            }
        }
        if (2 * i + 2 < array.length) {
            if (currentValue > array[2 * i + 2]) {
                return false;
            }
        }
    }
    return true;
}
```

TC & SC:

* O(n), O(1)
