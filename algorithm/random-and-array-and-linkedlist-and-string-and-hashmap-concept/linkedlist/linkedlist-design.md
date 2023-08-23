# LinkedList Design

## Design Single LinkedList



High Level



Middle Level:

* addHead/addTail/addIndex
* deleteHead/deleteTail/deleteIndex
  * 为啥deleteTail/deleteIndex会比较麻烦？
* size/isEmpty/get/getSize/searchByValue

TC\&SC: O(n)



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
    
    public ListNode searchByValue(int value){
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
        toBeDeletePrev.next = toBeDeletePrev.next.next;
        size--;
    }
}
</code></pre>





## Design Double LinkedList



High Level



Middle Level:

* addHead/addTail/addIndex
* deleteHead/deleteTail/deleteIndex
  * 为啥deleteTail/deleteIndex会比较麻烦？
* size/isEmpty/searchByValue

TC\&SC: O(n)

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
    ListNode tail;
    int size;
    
    public LinkedList(){
        this.head = null;
        this.tail = null;
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
        if (head == null) {
            head = newNode;
            tail = newNode;
        }
        else {
            newNode.next = head;
            head.prev = newNode;
            head = newNode;
        }
        size++
    }
    public void addTail(int val){
        ListNode newNode = ListNode(val);
        if (head == null) {
            head = newNode;
            tail = newNode;
        }
        else {
            tail.next = newNode;
            newNode.prev = tail;
            tail = newNode;
        }
        size++;
    }
    public void addIndex(int index, int val){
        if (index < 0 || index >= size) {
            return;
        }
        if (index == 0) {
            addHead(val);
        }
        if (index == size - 1) {
            addTail(val);
        }
        ListNode cur = head;
        ListNode newNode = new ListNode(val);
        for (int i = 0; i < index - 1; i++) {
            cur.next = cur;
        }
        ListNode prev = cur;
        ListNode next = cur.next;
        newNode.next = next;
        next.prev = newNode;
        prev.next = newNode;
        newNode.prev = prev;
        size++;  
    }
    // 删
    public void deleteHead() {
        if (head == null) {
            return;
        }
        if (head.next == null) {
            head = null;
            tail = null;
            size = 0;
            return;
        }
        ListNode newHead = head.next;
        newHead.prev = null;
        head.next = null;
        head = newHead;
        size--;
        return;
    }
    
    public void deleteTail() {
         if (head == null) {
            return;
        }
        if (head.next == null) {
            head = null;
            tail = null;
            size = 0;
            return;
        }
        ListNode temp = tail;
        tail = tail.prev;
        temp.prev = null;
        tail.next = null;
        size--;
    }
    
    public void deleteAtIndex(int index){
        if (index < 0 || index > size) {
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
        for (int i = 0; i < index - 1; i++){
            toBeDeletePrev = toBeDeletePrev.next;
        }
        ListNode prev = toBeDeletePrev.prev;
        ListNode next = toBeDeletePrev.next;
        prev.next = next;
        next.prev = prev;
        toBeDeletePrev.prev = null;
        toBeDeletePrev.next = null;
        size--;
    }
    public void deleteNode(ListNode toBeDeleted) {
        ListNode prevNode = toBedeleted.prev;
        ListNode nextNode = toBedeleted.next;
        if (prevNode == null) { //  toBedeleted is head
            ListNode temp = head;
            head = head.next;
            head.prev = null;
            temp.next = null;
        }
        if (nextNode == null) {
            ListNode temp = tail;
            tail = tail.prev;
            tail.next = null;
            temp.prev = null;
        }
        prev.next = nextNode;
        next.prev = prevNode;
        toBeDeletePrev.prev = null;
        toBeDeletePrev.next = null;
        size--;
    }
}
```





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
    
    public ListNode searchByValue(int value){
        ListNode cur = head;
        while (cur != null) {
            if (cur.value == value) {
                return cur;
            }
            cur = cur.next;
        }
        return null;
    }
    public ListNode get(int index) {
        
    }
    
    public getSize(){
        return this.size;
    }
    
    public boolean isEmpty(){
        return this.size == 0;
    }
    
    public void printAllNodes(){
        if (head == null) {
            return;
        }
        if 
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

}
```











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
    
    public ListNode searchByValue(int value){
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

}
```

[^1]: 
