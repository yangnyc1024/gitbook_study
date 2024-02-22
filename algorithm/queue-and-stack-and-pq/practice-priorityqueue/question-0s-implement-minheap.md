# Question 0s Implement MinHeap

<pre class="language-java"><code class="lang-java"><strong>public class minHeap{
</strong>    private int[] array;
    private int size; // size represents current # element
    
    public minHeap(int[] array) {
        // sanity check
        if (array == null || array.length == 0) {
            throw new IllegalArgumentException("input array cannot be null or empty");
        }
        this.array = array;
        this.size =  array.length;
        heapify();
    }
    
    public minHeap(int cap) {
        if (cap &#x3C;= 0) {
            throw new IllegalArguementException("capacity cannot be &#x3C;= 0")
        }
        array = new int[cap];
        size = 0;
        }
    
    private void heapify(){
        //for (int i = 0; i &#x3C; array.length /2; i++) {
           // percolateDown(i);
        //}
        for (int i = size / 2 - 1; i >= 0; i--) {
            percolateDown(i)
        }
    }
    
    // curIndex --- parent= (curIndex - 1) /2; 
    // curIndex --- leftChiIndex = curIndex * 2 + 1; rightChiIndex = curIndex * 2 + 2;
    private void percolateUp(int index) {
        if (index &#x3C; 0 &#x26;&#x26; index >= size) {
            throw new ArrayIndexOutOfBoundsException("invalid index range");
        }
        while (index > 0) {
            int pareIndex = (index - 1) / 2;
            if (array[pareIndex] > array[index]) {
                swap(pareIndex, index);
            } else {
                break;
            }
            index = pareIndex;
        }
    
    }
    
    private void percolateDown(int index) {
        if (index &#x3C; 0 &#x26;&#x26; index >= size) {
            throw new ArrayIndexOutOfBoundsException("invalid index range");
        }
        while (index &#x3C;= size / 2- 1) {
            int leftChiIndex = index * 2 +1;
            int rightChiIndex = index * 2 + 2;
            int candIndex = leftChiIndex;
            if (rightChiIndex &#x3C; size &#x26;&#x26; array[leftChiIndex] > array[rightChiIndex]) {
                candIndex  = rightChiIndex;
            }
            if (array[candIndex] &#x3C; array[index] {
                swap(candIndex, index);
            } else {
                break;
            }
            index = candIndex;
        }
    }
    
    public int peek() {
        if (size == 0) {
            throw new NoSuchElementException("heap is empty");
        }
        return array[0];
    }
    
    public int poll() {
        if (size == 0) {
            throw new NoSuchElementException("heap is empty");
        }    
        int ret = array[0];
        array[0] = array[size - 1];
        size--;
        percolateDown(0);
        // size--; // wrong!
    }
    
    public void offer(int ele) {
        if (size == array.length) {
            array = Arrays.copyof(array, (int)(array.length * 1.5));
        }
    
    }
    public int update(int index, int newValue) {
        if (index &#x3C;0 || index > size - 1) {
            throw new ArrayIndexOutOfBoundsException("invalid index range");
        }
        
        // update the value
        int oldValue = array[index];
        array[index] = newValue;
        
        // percolateDown &#x26; percolateUp
        if (oldValue &#x3C; newValue) {
            percolateDown(index);
        } else {
            percolateUp(index);
        }
        
        return oldValue;
    }
    
    private void swap(int left, int right) {
        int tmp = array[i];
        array[i] = array[j];
        array[j] = tmp;
    }
    public int size() {
        return size;
    }
    public boolean isEmpty() {
        return size == 0;
    }
    public boolean isFull() {
        return size == array.length;
    }
}
</code></pre>
