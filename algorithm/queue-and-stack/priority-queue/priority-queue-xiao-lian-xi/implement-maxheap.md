# Implement MaxHeap

```java
public class maxHeap {
    private int[] array;
    private int size;
    public maxHeap(int capacity) {
        this.array = new int[capacity];
        this.size = 0;
    }
    public maxHeap(int[] array) {
        this.array = array;
        this.size = array.length;
        heapify();
    }
    
    public int getSize() {
        return this.size;
    }
    
    public boolean isEmpty() {
        return this.size == 0;
    }
    
    public boolean isFull() {
        return this.size == array.length;
    }
    private void swap(int[] array, int i , int j) {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
    private void percolateDown(int index) {
        while (index * 2 + 2 <= this.size ) {
            // 换给谁
            int leftChild = index * 2 + 1;
            int rightChild = index * 2 + 2;
            int candidateChild = leftChild;
            if (rightChild < size && array[rightChild] > array[leftChild]) {
                candidateChild = rightChild;
            }
            //到底需不需要换
            if (array[index] < array[candidateChild]) {
                swap(array, index, candidateChild);
            }else {
                break;
            }
            index = candidateChild
        }
    }
    private void percolatedUp() {
    
    }
    private void heapify() {
    
    }
    
    public int poll() {
    
    }
    
    public int peek() {
    
    }
    
    public void offer() {
    
    }
    
    public int update() {
    
    }
}
```
