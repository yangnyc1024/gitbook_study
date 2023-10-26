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
        for (int i = 0 ; i < array.length; i++) {
            swap(array, 0, array.length - 1 - i);//这一步意味着倒数第i个元素已经完成了排序
            // 接下来调整0到array.length - 1 - i
            percolateDown(array, 0, array.length - 1 - i);
        }
    }
    int[] result = new int[k];
    for (int i = 0; i < k; i++) {
        result[i] = array[i];
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
        while (index* 2 + 2 <= size) {
            int leftChildIdx = 2 * index  + 1;
            int rightChildIdx = 2 * index + 2;
            int candidateIdx = leftChildIdx;
            if (rightChildIdx < size  && array[leftChildIdx] < array[rightChildIdx]) {
                candidateIdx = rightChildIdx;
            } 
            if (array[index] < array[candidateIdx]) {
                swap(array, index, candidateIdx);
            } else {
                break;
            }
            index = candidateIdx;
        }
    }
}
```

TC : O(n) + O()
