---
description: https://leetcode.com/problems/lru-cache/
---

# Problem 1 LRU cache

have been updated to new version

## What is cache

* 为了不每次都重新检索，所先把检索的结果存下来，下次用户访问的时候直接给存好的检索结果
* 想到的是Map\<key, value>, get a key by O(1)
* look up operation(memo)，如果计算过了，get上次计算的过，否则就重新算一遍
* Cache 的本质就是map，只不过区别是，他是一个<mark style="color:blue;">有capacity的map</mark>

## What is used:

* 所有的增改查insert, update query都是used
* put operation == insert/ update
* get operation == query
* remove operation == delete
* 注意，很多时候改，以为着是删/增

## 数据结构界的打工人：Map&#x20;

* Look up something（找什么，就是你所储存的东西） by something(透过什么来找，这个就是key)
* 经典的Use Case: 我需要知道我自己定义的Entry Reference在哪里，但是我propose的结果不具备优秀的查找功能
  * <mark style="color:red;">Map\<Key, Entry Reference> locationMap</mark>
  * key通过什么找reference，Entry Reference你其他的数据结构储存
* Example： Array Based PriorityQueue Update(key) Function
  * Map\<key, index> indexMapForKeyinHeap  + Heap
* 所有的操作，只要给我一个Key我都是可以拿到Entry Node, 又有了可以对时间排序的TreeSet/TreeMap

## Summary

* hybrid注意data structure, 先考虑每个元素cell里面有什么：
  * cell{key, value, index(hidden)}
* 再注意，多加结构的时候，必须用cell来做一个单位，会让思路更简单，比如说这道题如果用treeSet
  * map(key, <mark style="color:red;">cell</mark>) && container(<mark style="color:red;">cell</mark>)
  * <mark style="color:red;">并不能用map(key, index) && container(cell) , and Cell only have{key, index} ，why???</mark>
    * 因为如果你需要知道<mark style="color:red;">这个元素里的其他资料</mark>

```java
/*
Clarification:
	- get
		- given key, to see value
		- return the value
	- put
		- given key, to edit value
		- update key access order(arbitrary)
		- update key's value ==> update value(look up)
		- if key is in?
			- remove from container& map
			- insert
			- append()
		- if the cache limit is not reach && key not in?
			- insert(K, V)
			- put the element into the access order ==> append()
		- if the cache limit is reach && key in?
			- delete() LRU element => deleteMin() (access order) & remove from map
			- insert(K, V)
			- append()
High Level:
	- we need a ds to maintain the access order --- find a sorted order sorted
	- Map + TreeSet 

Middle Level:
	- Unsorted? Map/ set
		- map? Key, value? O(1)
		- Pop? Check all then pop , O (n)
	- Half sorted? TreeMap, heap
		- container(element),Element sorted by index?
		- Map<key/element,value>?
	- Sorted ? List? Doublelinkedlist
		- Element? Key,value, element 
		- Linkedlist<element>
		- Map<element, index>
TC& SC

*/

```





## Method 1 TreeSet/ TreeMap + Map

#### Step 1 Use Case API design



#### Step 2: Detail Logic

get(key):

* case 1 : map 里面有这个key
  * 透过Map拿到Entry node（return的data就在里面）
  * update这个Entry Node的时间信息（TreeSet里的这个Entry做update--> delete + insert）
* case 2: map里面没有这个key
  * return null
* overall: O(logn)

put(key, value):

* case 1: map 里面有这个key
  * 想当于update这个key-value pair里的value
  * 通过Map拿到Entry Node
    * update 这个Entry Node的value信息
    * update 这个Entry Node的时间信息
* case 2: map 里面没有这个key
  * case 2.1 现在没有满
    * 直接放一个新的Entry（update two maps）
  * case 2.2 现在满了
    * 踢出一个leat recently used：也就是TreeSet里面时间戳
* overall: O(logn)

timeStamp:&#x20;

* 设计为当前LRU class里的一个feild
* updated 准则，任何operation都需要update当前的信息

capacity:

* 设计为当前LRU class的一个field



* 注意put的details操作

#### TreeSet Version

````java
// Some code

// not correct

```java
```java
class LRUCache {
    private final int CAPACITY;
    private int timeStamp;
    private TreeSet<Entry> treeSet;
    private Map<Integer, Entry> map;
    public LRUCache(int capacity) {
        // assume cap valid
        this.CAPACITY = capacity;
        this.map = new HashMap<>();
        this.treeSet = new TreeSet<>();
        this.timeStamp = 0;
    }
    private void updateTimeStamp() {
        this.timeStamp++;
    }
    
    public int get(int key) {
        if (!map.containsKey(key)) {
            return -1;
        }
        Entry cur = map.get(key);
        treeSet.remove(cur);
        updateTimeStamp();
        cur.timeStamp = this.timeStamp;
        treeSet.add(cur);
        System.out.println(cur.value);
        return cur.value;
    }
    
    public void put(int key, int value) {
        if (map.containsKey(key)) {
            Entry cur = map.get(key);
            treeSet.remove(cur);
            updateTimeStamp();
            cur.timeStamp = this.timeStamp;
            cur.value = value;
            treeSet.add(cur);
            return;
        }
        else {
            updateTimeStamp();
            Entry newEntry = new Entry(key, value, timeStamp);
            if (treeSet.size() == CAPACITY) {
                Entry leastRecentUsedEntry = treeSet.first();
                treeSet.remove(leastRecentUsedEntry);
                map.remove(leastRecentUsedEntry.key);
            }
            map.put(key, newEntry);
            treeSet.add(newEntry);
        }
    }
    class Entry implements Comparable<Entry> {
        int timeStamp;
        int key;
        int value;
        public Entry(int key, int value, int timeStamp) {
            this.timeStamp = timeStamp;
            this.key = key;
            this.value = value;
        }
        @Override
        public int compareTo(Entry other) {
            return Integer.compare(this.timeStamp, other.timeStamp);
        }
    }
}
// class LRUCache {
// 	class Cell implements Comparable<Cell>{
// 		int key;
// 		int val;
// 		int index;
// 		Cell(int key, int val, int index) {
// 			this.key = key;
// 			this.val= val;
// 			this.index = index;
// 		}
// 		@Override
// 		public int compareTo(Cell that) {
// 			int result = Integer.compare(this.index, that.index);
// 			int result_b = Integer.compare(this.key, that.key);
// 			if (result == 0) {
// 				return result_b;
// 			}
// 			return result;
// 		}
// 	}
// 	HashMap<Integer, Cell> map; // key ->  Cell
// 	TreeSet<Cell> minSet; // key, Cell
// 	int count;
// 	int capacity;
//     public LRUCache(int capacity) {
//         this.capacity = capacity;
// 		map = new HashMap<>();
// 		minSet = new TreeSet<>();
//     }
    
//     public int get(int key) {
//         Cell cur = map.get(key);
// 		if (cur == null) {
// 			return -1;
// 		}
// 		int value = cur.val;
// 		minSet.remove(cur);
// 		count++;
// 		Cell newCur = new Cell(key, value, count);
// 		minSet.add(newCur);
// 		map.put(key, newCur);
// 		return value;
//     }
    
//     public void put(int key, int value) {
//         Cell cur = map.get(key);
// 	count++;
// 	if (cur != null) {
// 		minSet.remove(cur);
// 		map.remove(cur);
// 	}
// 	else if (cur == null && map.size() == capacity) {
// 		Cell needRemove = minSet.pollFirst();
// 		map.remove(needRemove.key);
// 	}
// 	Cell curNew = new Cell(key, value, count);
// 	minSet.add(curNew);
// 	map.put(key, curNew);
//     }
// }

````

#### TreeMap Version

````java
// Some code

class LRUCache {
    // treeMap version
    private final int CAPACITY;
    private int timeStamp;
    private Map<Integer, Integer> cache;
    private TreeMap<Integer, Entry> timeOrder; // TreeMap key is timeStamp
    public LRUCache(int capacity) {
        this.timeStamp = -1;
        this.cache = new HashMap<>();
        this.timeOrder = new TreeMap<>();
        this.CAPACITY = capacity;
    }
    
    public int get(int key) {
        if (cache.containsKey(key)) {
            Integer timeStamp = cache.get(key);
            Entry pair = timeOrder.get(timeStamp);
            increaseTimeStamp();
            updateTimeOrder(timeStamp, pair);
            return pair.getValue();
        }
        else {
            return -1;
        }
    }
    private void increaseTimeStamp() {
        this.timeStamp++;
    }
    private int getTimeStamp(){
        return this.timeStamp;
    }
    private int getCap() {
        return this.CAPACITY;
    }
    private void evictOldest(int time){
        Entry old = timeOrder.get(time);
        this.timeOrder.remove(time);
        this.cache.remove(old.getKey());
    }
    private void updateTimeOrder(int timeStamp, Entry pair) {
        evictOldest(timeStamp);
        timeOrder.put(getTimeStamp(), pair);
        cache.put(pair.getKey(), getTimeStamp());
    }
    private void addToCache(int currentTime, Entry pair) {
        timeOrder.put(currentTime, pair);
        cache.put(pair.getKey(), currentTime);
    }
    
    public void put(int key, int value) {
        if (cache.containsKey(key)) {
            Integer timeStamp = cache.get(key);
            Entry pair = timeOrder.get(timeStamp);
            pair.setValue(value);
            increaseTimeStamp();
            updateTimeOrder(timeStamp,pair);
        }
        else {
            Entry pair = new Entry(key, value);
            increaseTimeStamp();
            int time = getTimeStamp();
            if (isEmpty()) {
                addToCache(time, pair);
                return;
            }
            if (isFull()) {
                Integer oldestPairTimeStamp = timeOrder.firstKey();
                evictOldest(oldestPairTimeStamp);
            }
            addToCache(time, pair);
        }
    }
    public boolean isFull() {
        return getSize() == getCap();
    }
    public boolean isEmpty() {
        return getSize() == 0;
    }
    private int getSize() {
        return this.cache.size();
    }
    class Entry {
        private int key;
        private int value;
        public Entry(int key, int value) {
            this.key = key;
            this.value = value;
        }
        public int getKey() {
            return this.key;
        }
        public int getValue() {
            return this.value;
        }
        public void setKey(int key) {
            this.key = key;
        }
        public void setValue(int value) {
            this.value = value;
        }
    }
}
```
````



## Method 2 DoubleLinkedList

* <mark style="color:blue;">除了treeSet还有什么数据结构可以保持时间顺序？              Queue==> FIFO时间顺序</mark>
* <mark style="color:blue;">Queue逻辑上的数据结构 =>  怎么实现Queue</mark>
  * Queue\<Integer> queue = new ArrayDeque<>();
  * Queue\<Integer> queue = new LinkedList<>();
* <mark style="color:blue;">增删改查全是O(1)</mark>
  * **Queue是逻辑数据结构，底层实现的是LinkedList**
  * 而DoubleLinkedList是因为O(1)的删除
* 那你得给我这个node reference，有了这个node reference,我做什么都是O(1),关键问题是，人家User insert/update/remove/query，人家给你的是key，不是node reference
* **打工人上线: Map\<Key, DoublyListNode> locationMap + DoubleLinkedList(datainfo) DLL**

#### Step 1 Use Case API design

* get(key)
* put(key, value)

#### Step 2: Detail Logic

get(key):&#x20;

* case 1 : map 里面有这个key
  * get the key==>  通过map拿到装有data的ListNode ==> ListNode里面的东西就是return的东西
  * update time order ==> remove this ListNode from LinkedList, then insert into Head
* case 2: map里面没有这个key
  * return null
* overall: O(logn)

put(key, value):

* case 1: map 里面有这个key
  * update the value ==> 通过map拿到装有data的ListNode  ==》 update ListNode
  * update the order ==> remove this ListNode from LinkedList, then insert into head
* case 2: map 里面没有这个key
  * case 2.1 the cache is not full (check map 的size到不到capacity)
    * put the key value there
    * update the time order ==> insert into Head
  * case 2.2 现在满了
    * delete the oldest one ==> 踢出tail node
    * put the kye value there ==> insert into map and LL
    * update the time order ==> head
* overall: O(1)

timeStamp:&#x20;

* 设计为当前LRU class里的一个feild
* updated 准则，任何operation都需要update当前的信息

capacity

* 设计为当前LRU class的一个field

````java

import static java.lang.Math.nextDown;

/*
Element: <key, value, timeStamp>
<key, Element>
<Element_1> --> <Element_2>
get: given a key to see if we can find the value in the container(using the lookupMap check)
 in? find this element, rand update its timeStamp, put it back
 not? reutrn -1
put: given a key and value  
- container this key, find this element, update its value& timeStamp, and put it back
- not container, 
    - if reach the capacity, delete the least element
    - put this element into the container

*/


class LRUCache {
    // class Node implements Comparable<Node> {
    class Node {
        int key;
        int value;
        int timeStamp;
        Node prev;
        Node next;
        // public Node (int key, int value, int timeStamp) {
        public Node (int key, int value) {
            this.key = key;
            this.value = value;
            // this.timeStamp = timeStamp;
        }
        // @Override
        // public int compareTo(Node that) {
        //     return Integer.compare(this.timeStamp, that.timeStamp);
        // }
    }

    private Node head;
    private Node tail;
    private Map<Integer, Node> map;
    private final int CAPACITY;
    public LRUCache(int capacity) {
        this.CAPACITY = capacity;
        this.map = new HashMap<>();
    }
    
    public int get(int key) {
        if (!map.containsKey(key)) {
            return -1;
        }
        Node cur = map.get(key);
        deleteNode(cur);
        addNode(cur);
        return cur.value;
    }
    
    public void put(int key, int value) {
        if (map.containsKey(key)) {
            Node cur = map.get(key);
            cur.value = value;
            deleteNode(cur);
            addNode(cur);
        } else {
            if (map.size() == this.CAPACITY) {
                deleteNode(tail);
            }
            addNode(new Node(key, value));
        }
    }
    private void deleteNode(Node node)  {
        map.remove(node.key);
        if (node.prev != null && node.next != null) {
            Node prevNode = node.prev;
            Node nextNode = node.next;
            prevNode.next = nextNode;
            nextNode.prev = prevNode;
        }
        else if (node.prev == null && node.next != null) { // node = head, more than 2 node
            head = node.next;
            head.prev = null;
        }
        else if (node.prev != null && node.next == null) { // node = tail, more than 2 node
            tail = node.prev;
            tail.next = null;
        } else { // node = head = tail, only 1 element
            head = tail = null;
        }
        node.prev = node.next = null;
    }

    private void addNode(Node node)  {
        map.put(node.key, node);
        if (head == null) {
            head = tail = node;
        } else {
            node.next = head;
            head.prev = node;
            head = node;
        }
    }
}
```
````
