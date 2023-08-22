# LinkedList Design

## Design Single LinkedList

<pre class="language-java"><code class="lang-java">class ListNode{ 
    int value;
    ListNode next;
    
    @Override
    public String toString() {
        return "this value : " + value;
    }
}

class LinkedList {
    // Field 属性：静态的属性
    // Method 行为：动态的行为
    ListNode head;
    int size;
    
    public LinkedList(){
        this.head = null;
        this.size = 0;
    }
    
    public ListNode seachByValue(int value){
        ListNode cur = head;
        while (cur != null) {
            if (cur.value == value) {
                return cur;
            }
            cur = cur.next;
        }
        return null;
    }
    
    public getSize(){
        return this.size;
    }
    
    public boolean isEmpty(){
        return this.size == 0;
    }
    
    public void printAllNodes(){
        ListNode cur = head;
        while (cur != null) {
            System.out.println(cur);
            cur = cur.next;
        }
    }
    
    // 增
    public void addHead(int val){
        ListNode newNode = new ListNode(val);
        newNode.next = head;
        head = newNode;
        size++;
    }
    public void addTail(int val){
        ListNode newNode = ListNode(val);
        if (head == null) {
            head = newNode;
        }
        else {
            ListNode cur = head;
            while (cur.next != null) {
                cur = cur.next;
            }
        }
        size++;
    }
    public void addIndex(int index, int val){
        if (index &#x3C; 0 || index >= size) {
            return;
        }
        if (index == 0) {
            addHead(val);
            return;
        }
        if (index == size - 1) {
            addTail(val);
            return;
        }
        ListNode cur = head;
        ListNode newNode = new ListNode(val);
        //要想在index 这个位置插入一个node，需要找到index -1的这个node，然后在这个node之后加入新的node
        for (int i = 0; i &#x3C; index - 1; i++) {
           cur = cur.next;  
        }
        //在中间插入node的方法一定是 先保留后面的node 再做插入
        newNode.next = cur.next;
        cur.next = newNode;
        size+=;
    }
    // 删
    public void deleteHead() {
        if (head == null) {
            return;
        }
        head = head.next;
        size--;
    }
    <a data-footnote-ref href="#user-content-fn-1">public void deleteTail() {</a>
        if (head == null) {
            return;
        }
        if (head.next == null) {
            deleteHead();
            return;
        }
        ListNode cur = head;
        ListNode nextNode = head.next;
        while (cur.next != null &#x26;&#x26; nextNode.next != null) {
            cur = cur.next;
            nextNode = nextNode.next;
        }
        cur.next = null;
        // ListNode prev = null;
        // ListNode cur = head;
        // while(cur.next != null) {
            //现在的cur，就是下一轮的prev
            //prev = cur;
            //cur = cur.next;
        //}
        // prev.next = null;
        size--;
    }
    
    public void deleteAtIndex(int index){
        if (index &#x3C; 0 || index > size) {
            return;
        }
        if (index == 0) {
            deleteHead();
            return;
        }
        if (index == size - 1) {
            deleteTail();
            return;
        }
        ListNode toBeDeletePrev = head;
        for (int i = 0; i &#x3C; index - 1; i++){
            toBeDeletePrev = toBeDeletePrev.next;
        }
        toBeDeletePrev.next = toBeDeletePrev.next.nextl
        size--;
    }

}
</code></pre>





## Design Double LinkedList







## Design Circular LinkedList















```java
class ListNode{ 
    int value;
    ListNode next;
    
    @Override
    public String toString() {
        return "this value : " + value;
    }
}

class LinkedList {
    // Field 属性：静态的属性
    // Method 行为：动态的行为
    ListNode head;
    int size;
    
    public LinkedList(){
        this.head = null;
        this.size = 0;
    }
    
    public ListNode seachByValue(int value){
        ListNode cur = head;
        while (cur != null) {
            if (cur.value == value) {
                return cur;
            }
            cur = cur.next;
        }
        return null;
    }
    
    public getSize(){
    
    }
    
    public boolean isEmpty(){
    
    }
    
    public void printAllNodes(){
    }
    
    // 增
    public void addHead(){
    
    }
    public void addTail(){
    
    }
    public void addIndex(int index, int val){
    
    }
    // 删
    public void deleteHead() {
    
    }
    public void deleteTail() {
    
    }
    
    public void deleteAtIndex(int index){
    
    }

}java
```

[^1]: 
