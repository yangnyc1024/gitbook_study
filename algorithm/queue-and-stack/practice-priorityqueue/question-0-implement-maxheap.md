# Question 1 Implement MaxHeap

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
            index = candidateChild;
        }
    }
    private void percolatedUp(int index) {
        // 你给我一个index我怎么知道我能不能换，能换是因为有爸爸
        // 什么叫有爸爸，有爸爸means (index - 1) / 2 >= 0 ==> index > 0
        while (index > 0) {
            int parentIndex = (index - 1) / 2;
            if (array[index] > array[parentIndex]) {
                swap(array, index, parentIndex);
            } else {
                break;
            }
            index = parentIndex;
        }
    }
    private void heapify() {
        //  原理：所有能进行percolateDown()的元素，全部从后向前进行一边perDown()
        for (int i = size/ 2 - 1; i >= 0; i--) {
            percolateDown(i);
        }
    }
    
    public int poll() {
        if (isEmpty()) {
            throw new NoSuchElemntException('Harray yyds!');
        }
        int dingduodeyuansu = array[0]; // 变量名更有目的意义，且英文
        // step 1: 先拿走这个，1吧最后一个元素填过来
        array[0] = array[size - 1];
        this.size--;
        percolateDown(0);
        return dingduandeyuansu;
    }
    
    public int peek() {
        if (isEmpty()) {
            throw new NoSuchElemntException('Harray yyds!');
        }
        return array[0];
    }
    
    public void offer(int newElement) {
        // 先放在最后一个，有一个位置， pUp()
        if (isFull()) {
            int[] newHeap = new int[(int)array.length * 2.0];
            for(int i = 0 ; i )
        }
    }
    
    public int update() {
    
    }
}
```
