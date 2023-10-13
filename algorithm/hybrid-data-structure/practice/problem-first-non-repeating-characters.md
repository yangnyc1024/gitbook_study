# Problem First Non-Repeating Characters

* use case: O(1) time + first
* 关键词，first: 必须keep时序
* O(1) time: Map(Key: Character, Value: ListNode) + DLL as Queue
* 这和LRU的区别点是什么？
  * 识别那些character是non repeating，
  * 一个字母已经出现了2次vs这个字母一次都没有出现---》你怎么知道踢了vs还是放进去





## Option 1: double linkedlist + map + set

<figure><img src="../../.gitbook/assets/Screenshot 2023-10-13 at 9.04.36 AM.png" alt=""><figcaption></figcaption></figure>

API 1: new coming character:

* double linkedlist==> 最快做删除 ==> 找到自己就能找到前一个和后一个==> 添加和删除都是O(1）的时间
* Look up operation ==> Map\<Character, ListNode> ==> 很快找到ListNode\
  \==> Set\<Character>==> help determine repeat
* 分析
  * case 1先确认这个字母在不在set里，如果存在，直接ignore
  * case 2如果不在set里面
    * case2.1再看map，如果这个字母不在map里面
      * 这是我们第一次遇到这个字母，update Map + DLL
    * case2.2如果这个字母在map里面
      * 说明这个字母发生了重复，remove it from Map +DLL, add it to repeating set



API 2: who is the first?

* 看看你define的DLL里哪一段是代表时间序列

```java
// Some code

public class Solution{
    static class Node {
        Node prev;
        Node next;
        Character ch;
        Node(Character ch) {
            this.ch;
        }
    }
    private Node head;
    private Node tail;
    private Set<Character> repeated;
    private Map<Character, Node> singled;
    public Solution() {
        head =  new Node(null);
        head.prev = head.next = head;
        tail = head;
        repeated = new HashSet<>();
        singled = new HashMap<>();
    }
    public void read(char ch){
        // if the character already exists more than once ==> ignore
        if (repeated.contains(ch)) {
            return;
        }
        
        Node node = singled.get(ch);
        // if the character appears for the first time ==> add to the list and the nonrepeated 
        if (node == null) {
            node = new Node(ch);
            append(Node);
        }
        // if the character is already in the nonrepeated ==> remove it from the map and list
        // put it into the repeat set
        else {
            remove(Node);
        }
    }
    private void append(Node node){
        // append to map
        // append to the DLL
        singled.put(node.ch, node);
        tail.next = node;
        node.prev = tail
        node.next = head;
        tail = tail.next;
    }
    
    
    private void remove(Node node) {
        // remove from the map
        // add to repeat set
        // remove from DLL
        node.prev.next = node.next;
        node.next.prev = node.prev;
        if (node == tail) {
            tail = node.prev;
        }
        node.prev = node.next = null;
        singled.remove(node.ch);
        repreated.add(node.ch);
        
    }
    
    private Character firstNonRepeating() {
        if (head == tail) {
            return null;
        }
        return head.next.ch;
    }
}
```



## Option 2: double linkedlist + map



API 1: new coming character:

* double linkedlist==> 最快做删除 ==> 找到自己就能找到前一个和后一个==> 添加和删除都是O(1）的时间
* Look up operation ==> Map\<Character, ListNode> ==> 很快找到ListNode\
  \==> Set\<Character>==> help determine repeat
* 分析
  * c<mark style="color:blue;">ase 1先确认这个字母在不在map里</mark>
    * <mark style="color:blue;">如果存在对用的是reference node 是null，直接ignore</mark>
  * case 2如果不在set里面
    * case2.1再看map，如果这个字母不在map里面
      * 这是我们第一次遇到这个字母，如果这个字母不在map里面
    * case2.2如果这个字母在map里面
      * <mark style="color:blue;">如果是多次出现的字母，map里存的是这个字母的marker(mark this character already repeat)</mark>
        * <mark style="color:blue;">use Null as special value</mark>



API 2: who is the first?

* 看看你define的DLL里哪一段是代表时间序列
