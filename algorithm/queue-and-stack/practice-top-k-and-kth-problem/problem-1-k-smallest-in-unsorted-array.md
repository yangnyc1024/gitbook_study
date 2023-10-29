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
public int[] kSmallest(int[] array, int k) {
    // sanity check
    int[] result = new int[k];
    
    // step 1: heapify all elements in array
    heapify(array);
    
    // step 2: each time poll out the first one
        // poll the first element in the array until we get k elements
        // swap the first and the array.length - 1 - i element;
        // percolateDown the first element;
    
    for (int i = 0; i < k; i ++) {
        result[i] = array[0];
        swap(array, 0, array.length - 1 - i);
        percolateDown(array, i, array.length - i); // the last element is size
    }
    return result;
}

private void heapify(int[] array) {
    for (int i = array/ 2 - 1; i >= 0; i++) {
        percolateDown(array, i , array.length);
    }
}

private void swap(int[] array, int i, int j) {
    int temp = array[i];
    array[i] = array[j];
    array[j] = temp;
}
private void percolateDown(int[] array, int index, int size) { //这里的size是0，size-1的点
    while (index * 2 + 2 <= size) {
        int leftChild = 2 * index + 1;
        int rightChild = 2 * index + 2;
        int candidate = leftChild;
        if (rightChild < size. && array[leftChild] < array[rightChild]) {
            candidate = rightChild;
        }
        if (array[index] < array[candidate]) {
            swap(arary, index, candidate);
        } else {
            break;
        }
        index = candidate;
    } 
}
```

TC: O(n + k logn)

SC: O(1)



#### Method 3: MaxHeap（两种）

方法论：当题目求的topK和Kth和你的Heap比较的优先级不一样

* 你的heap里装的是：<mark style="color:red;">到目前为止</mark><mark style="color:purple;">topK candidate</mark>
  * 手头先攥k个，这些是候选人
  * 然后再撸那些没看过的元素，如果你看到更优先，我们得淘汰手头最不优先的

```java
public class KSmallest{
    
    public int[] kSmallest(int[] array, int k) {
        // sanity check
        if (array.length == 0 || k == 0) {
            return new int[]{0};
        }
        // build the pq
        //PriorityQueue<Integer> maxHeap = new PriorityQueue<Integer>(k , new Comparator<Integer>() {
            //@Override
            //public int compare(Integer o1, Integer o2) {
                //if (o1.equals(o2) {
                    //return 0;
                //}
                //return o1 > o2 ? -1: 1;
            //}
        //})        
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collection.reverseOrder());
        
        // offer pq in and poll when pq.size() > k
        //for (int i = 0; i < array.length; i++) {
            //if (i < k) {
               // maxHeap.offer(array[i]);
            //}
            //else if (array[i] < maxHeap.peek()) {
                //maxHeap.poll();
                //maxHeap.offer(array[i]);
            //}
        //}    
        for (int i = 0; i < array.length; i++) {
            maxHeap.offer(array[i]);
            if (maxHeap.size() > k) {
                maxHeap.poll();
            }
        }  
        
        // post processing return all result
        
        int[] result = new int[k];
        for (int i = k -1; i >= 0; i--) {
            result[i] = maxHeap.poll();
        }
        return result;
    }
}
```

这个方法能用heapify优化么？

* 这个方法是把前k个元素放到heap里，是k size heap
* heapify应该是O(k)，不应该是O(n)---> 我们只应该heapify前k个元素)
* \---> 本质上实现一个带range的heapify

```java
public int[] kSmallest(int[] array, int k) {
    heapify(array, 0 , k -1);
    // step 1: build the similuated heap in [0, k- 1]
    
    // step 2: try to find the good candidate if array[new] < array[0]
        // swap, percolatedDown
    // step 3:
        // get the result out from small to large 
        // 你应该每次都是从0th拿出来，但是还是需要percolateDown

}
```

TC: O(k + (n - k) log k)

SC: O(1)

* &#x20;拓展：percolate and heapify只针对left = 0的代码
  * 如果你想要拓展，必须保证left对应第一个元素，采用offset或者\[left, right]
* This one also works for online algorithm
* 体现出实时性，如果不需要读完完整的input就可以实时的知道，到目前为止的结果，这就是online算法。不然我们就称之为offline算法
