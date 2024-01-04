# Problem 2 Kth Largest Element in an Array

#### Method 1: MaxHeap

全部放进去弄k次

```java
public int findKthLargest(int[] nums, int k) {
    // assume nums not null and empty
    PriortyQueue<Integer> maxHeap = new PriortyQueue<>(Collections.reverseOrder());
    for (int i = 0; i < nums.length; i++) {
        maxHeap.offer(nums[i]);
    }
    int count = k;
    while (count > 1) {
        maxHeap.poll();
        count--;
    }
    return maxHeap.peek();
}
```



#### Method 2: MinHeap

先手头拿K个candidate，

然后在便利接下来n-k个，看看能不能淘汰手头不优先的



```java
public int findKthLargest(int[] nums, int k) {
    // assume nums not null and empty
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    for (int i = 0; i < nums.length; i++) {
        if (minHeap.size() < k) {
            minHeap.offer(nums[i]);
        }
        else if (minHeap.peek() < nums[i]) {
            minHeap.poll();
            minHeap.offer(nums[i]);
        }
    }
    return minHeap.peek();
}


public int findKthLargest(int[] nums, int k) {
    // assume nums not null and empty
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    for (int i = 0; i < nums.length; i++) {
        minHeap.offer(nums[i]);
        if (minHeap.size() > k) {
            minHeap.poll();
        }
    }
    return minHeap.peek();
}
```

TC: O(nlogK)

SC: O(logn)



这个minHeap online的算法能优化么？如果input是一个array，arraylist一定能用heapify优化



```java
public int findKthLargest(int[] nums, int k) {
    heapify(array, 0, k -1);
    for (int i = k; i < array.length; i++) {
        if (array[i] > array[0]) {
            swap(array, 0, i);
            percolateDown(array, 0 , k);
        }
    }
    return array[0];
}

private void heapify(int[] array, int left, int right) {
    int size = right - left + 1;
    for (int i = size /2 -1 ; i >=0; i--) {
        percolateDown(array, i, size);
    }
}
private void percolateDown(int[] array, int index, int size) {
    while (2 * index + 2 < size) {
        int leftIndex = 2 * index + 1;
        int rightIndex = 2 * index + 2;
        int candidate = leftIndex;
        if (rightIndex < size && array[rightIndex] < array[leftIndex]) {
            candidate = rightIndex;
        }
        if (array[candidate] < array[index]) {
            swap(array, candidate, index);
        }else {
            break;
        }
        index = candidate;
    }
}
private void swap(int[] array, int left, int right) {
    int temp = array[left];
    array[left] = array[right];
    array[right] = temp;
}
```
