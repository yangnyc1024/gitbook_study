# Problem 1 K smallest In Unsorted Array

#### Method 1: Sorting&#x20;

* (体会下考点不再这里)==》 面试里提一个即可，不要浪费时间

High Level:

* 把数组从小到大排列
* 前k个元素就是最小的k个元素

TC& SC

* O(nlogn), O(sort)

```java
public class Solution {
    public int[] kSmallest(int[] array, int k) {
        Arrays.sort(array);
        int[] result = new int[k];
        for (int i = 0; i< k; i++) {
            result[i] = array[i];
        }
        return result;
    }
}
```

#### Method 1b: 用heap sort，不用API

* 我要用Heap Sort,不用API
  * step 1:  开个heap
  * step 2: 把所有的元素都放在heap里,再拿出来一遍
* 这个方法不是heap sort，heap sort的最大的优势
  * 不仅是可以和mergeSort一样能达到nlogn的时间
  * 而且人家是space O(1)

```java
class solution {
    public int[] kSmallest(int[] array, int k) {
        heapify(array); // 把你给我的array变成一个heap 
            // 你heap完没有按顺序啊，所以我每次只能拿出来在最前面的那个
            // 所以后面每一步，我需要从第0个，一个个percolateDown，确保从第0个到第k-1个都是排好序的
        for (int i = 0 ; i < array.length; i++) {
            swap(array, 0, array.length - 1 - i);//这一步意味着倒数第i个元素已经完成了排序
            // 接下来调整0到array.length - 1 - i
            percolateDown(array, 0, array.length - 1 - i);
        }
        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = array[i];
        }
    }
    private void heapify(int[] arr) {
        for (int i = arr.length/ 2 - i ; i >= 0; i--) {
            percolateDown(arr, i, arr.length);
        }
    }
    private void swap (int[] arr, int i , int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    private void percolateDown(int[] array, int index, int size) {
        while ( 2* index + 2 <= size) {
            int leftChild = 2 * index + 1;
            int rightChild = 2 * index + 2;
            int candidateChild = leftChild;
            if (rightChild <= size && array[rightChild] > array[leftChild]) {
                candidateChild = rightChild;
            }
            if (array[index] > array[candidateChild]){
                swap(array, index, candidateChild);
            } else{
                break;
            }
            index = candidateChild;
        }
    }
}
```

TC : O(n) + O(klogn) + O(k) ==> O(nlogn)

SC: O(1)





#### Method 2 MinHeap（两种）

方法论：当题目求的topK和Kth和你的heap比较的优先级一致的时候，全放进去，poll K次

* TC: O(nlogn)
* SC: O(n)



```java
public int[] kSmallest(int[] array, int k) {
    PriorityQueue<Integer> minHeap = new ArrayQueue<>();
    for (int num: array) {
        minHeap.offer(num);
    }
    int[] result = new int[Math.min(minHeap.size()),k];
    for(int i = 0; i < result.length; i++) {
        result[i] = minHeap.poll();
    }
    return result;
}
```



* 自己实现heapify且直接poll up前k个
* 和前面不一样，前面那个是sort好，再解决，这个是每次都poll直到第k次，所以时间会变成O(klog n)



```java
public int[] kSmallest(int[] array, int k)
```

TC: O(n + k logn)

SC: O(1)





#### Method 3: MaxHeap（两种）

方法论：当题目求的topK和Kth和你的Heap比较的优先级不一样

* 你的heap里装的是：<mark style="color:red;">到目前为止</mark><mark style="color:purple;">topK candidate</mark>
  * 手头先攥k个，这些是候选人
  * 然后再撸那些没看过的元素，如果你看到更优先，我们得淘汰手头最不优先的

```java
```

这个方法能用heapify优化么？

* 这个方法是把前k个元素放到heap里，是k size heap
* heapify应该是O(k)，不应该是O(n)---> 我们只应该heapify前k个元素)
* \---> 本质上实现一个带range的heapify

```java
```

