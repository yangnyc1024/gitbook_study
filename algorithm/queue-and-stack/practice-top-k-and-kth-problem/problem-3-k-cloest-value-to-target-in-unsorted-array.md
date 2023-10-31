# Problem 3 K Cloest Value to Target in Unsorted Array

#### Method 1: Sort



#### Method Optimal:&#x20;

* 脱马甲，online algorithm use an maxHeap to store the element and the absolut diff
* K smallest Absolute Diff value to target
* Use MaxHeap：到目前为止的前K近的数



```java
class Pair {
    private int diff;
    private int value;
    public Pair(int diff, int value) {
        this.diff = diff;
        this.value = value;
    }
    public int getValue(){
        return this.value;
    }
}

public int[] findKCloset(int[] array, int k , int target) {
    // assume all input argument are valid
    if (array == null || array.length == 0 || k > array.length || k < 0) {
        return array;
    }
    int[] result = new int[k];
    PriorityQueue<Pair> maxHeap = new PriorityQueue<>(
        (pairOne, pairTwo) -> Integer.compare(pairTwo.diff, pariOne.diff);
    )
    for (int i = 0; i < array.length; i++) {
        int diff = Math.abs(array[i] - target);
        maxHeap.offer(new Pair(diff, array[i]));
        if (maxHeap.size() > k) {
            maxHeap.poll();
        }
    } 
    int index = 0;
    for (int i = 0; i < k; i++) {
        result[index] = maxHeap.poll().getValue();
        index++;
    }
    return result;
}
```

#### Method 3: use MinHeap
