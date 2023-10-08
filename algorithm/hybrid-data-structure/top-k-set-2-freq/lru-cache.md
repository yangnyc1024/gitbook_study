---
description: https://leetcode.com/problems/lru-cache/
---

# LRU cache



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
  * Map\<Key, Entry Reference> locationMap
  * key通过什么找reference，Entry Reference你其他的数据结构储存
* Example： Array Based PriorityQueue Update(key) Function
  * Map\<key, index> indexMapForKeyinHeap  + Heap
* 所有的操作，只要给我一个Key我都是可以拿到Entry Node, 又有了可以对时间排序的TreeSet/TreeMap

## Summary

* hybrid注意data structure, 先考虑每个元素cell里面有什么：
  * cell{key, value, index(hidden)}
* 再注意，多加结构的时候，必须用cell来做一个单位，会让思路更简单，比如说这道题如果用treeSet
  * map(key, <mark style="color:red;">cell</mark>) && container(<mark style="color:red;">cell</mark>)
  * 并不能用<mark style="color:yellow;">map(key, index)</mark> && container(cell) , and <mark style="color:yellow;">Cell only have{key, index} ，why???</mark>





## Method 1 TreeSet/ TreeMap + Map

#### Step 1 Use Case API design



#### Step 2: Detail Logic

get(key):&#x20;

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

capacity

* 设计为当前LRU class的一个field



* 注意put的details操作

```java
/*
Clarification:
	- get
		- update key access order
		- return the value
	- put
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

class LRUCache {
	class Cell implements Comparable<Cell>{
		int key;
		int val;
		int index;
		Cell(int key, int val, int index) {
			this.key = key;
			this.val= val;
			this.index = index;
		}
		@Override
		public int compareTo(Cell that) {
			int result = Integer.compare(this.index, that.index);
			int result_b = Integer.compare(this.key, that.key);
			if (result == 0) {
				return result_b;
			}
			return result;
		}
	}
	HashMap<Integer, Cell> map; // key ->  Cell
	TreeSet<Cell> minSet; // key, Cell
	int count;
	int capacity;
    public LRUCache(int capacity) {
        this.capacity = capacity;
		map = new HashMap<>();
		minSet = new TreeSet<>();
    }
    
    public int get(int key) {
        Cell cur = map.get(key);
		if (cur == null) {
			return -1;
		}
		int value = cur.val;
		minSet.remove(cur);
		count++;
		Cell newCur = new Cell(key, value, count);
		minSet.add(newCur);
		map.put(key, newCur);
		return value;
    }
    
    public void put(int key, int value) {
        Cell cur = map.get(key);
	count++;
	if (cur != null) {
		minSet.remove(cur);
		map.remove(cur);
	}
	else if (cur == null && map.size() == capacity) {
		Cell needRemove = minSet.pollFirst();
		map.remove(needRemove.key);
	}
	Cell curNew = new Cell(key, value, count);
	minSet.add(curNew);
	map.put(key, curNew);
    }
}
```

## Method 2 DoubleLinkedList

* 除了treeSet还有什么数据结构可以保持时间顺序？-----Queue=》 FIFO时间顺序
* Queue逻辑上的数据结构==〉 怎么实现Queue
  * Queue\<Integer> queue = new ArrayDeque<>();
  * Queue\<Integer> queue = new LinkedList<>();
* 增删改查全是O(1)
  * Queue是逻辑数据结构，底层实现的是LinkedList
  * 而DoubleLinkedList是因为O(1)的删除
* 那你得给我这个node reference，有了这个node reference,我做什么都是O(1),关键问题是，人家User insert/update/remove/query，人家给你的是key，不是node reference
* 打工人上线: Map\<Key, DoublyListNode> locationMap + DoubleLinkedList(datainfo) DLL

#### Step 1 Use Case API design

* get
* put

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

```java

class LRUCache {

  // map: key: key, value: DLinkedNode
  // DLinkedNode: key, value, prevNode, nextNode
    // 记得两个一起操作

    private class DLinkedNode {
        int key;
        int value;
        DLinkedNode prev;
        DLinkedNode next;
        // public DLinkedNode(int key, int value) {
        //     this.key = key;
        //     this.value = value;
        // }
    }
    private int capacity;
    private Map<Integer, DLinkedNode> map = new HashMap<>();
    private DLinkedNode head; // head -> last element // head 一般都是新加的
    private DLinkedNode tail; // tail -> first element to could be delete

    public LRUCache(int capacity) {
        this.capacity = capacity;
        // DLinkedNode head = new DLinkedNode(-1, -1); //这样不赋值啊！！！！不是同一个head
        // DLinkedNode tail = new DLinkedNode(-1, -5);
        this.head = new DLinkedNode();
        this.tail = new DLinkedNode();
        head.next = tail;
        tail.prev = head;

    }
    
    public int get(int key) {
      // get from map
      // delete it from the doublelinklist
      // return 
        DLinkedNode cur= map.get(key); //不需要删，而是更新位置
        if (cur == null) return -1;
        deleteNode(cur);
        addNode(cur);
        return cur.value;

    }
    
    public void put(int key, int value) {
        DLinkedNode potentialNode = map.get(key);
        if (potentialNode != null) {
            potentialNode.value = value;
            deleteNode(potentialNode);
            addNode(potentialNode);
        }
        else {
            DLinkedNode curNode = new DLinkedNode();
            curNode.key = key;
            curNode.value = value;
            map.put(key, curNode);  // add in map
            addNode(curNode);  // add in doubleLinedList
            if (map.size() > capacity) {
                DLinkedNode deleteNode = tail.prev;
                deleteNode(deleteNode);
                map.remove(deleteNode.key);
            }
        }
    }
    
    private void deleteNode(DLinkedNode curNode) {
        DLinkedNode prevNode = curNode.prev;
        DLinkedNode nextNode = curNode.next;
        prevNode.next = nextNode;
        nextNode.prev = prevNode;
        curNode.prev = null;
        curNode.next = null;
    }

    private void addNode(DLinkedNode curNode) {
        DLinkedNode next = head.next;
        head.next = curNode;
        curNode.prev = head;
        curNode.next = next;
        next.prev = curNode;
        // curNode.prev = head;
        // curNode.next = head.next;
        // head.next.prev = curNode;
        // head.next = curNode;

    }

}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

Method 3 TreeMap
