# LinkedList Design

## Design Single LinkedList

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
        return this.size;
    }
    
    public boolean isEmpty(){
        return this.size == 0;
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
