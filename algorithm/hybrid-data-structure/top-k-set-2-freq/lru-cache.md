---
description: https://leetcode.com/problems/lru-cache/
---

# LRU cache

## Summary

* hybrid注意data structure, 先考虑每个元素cell里面有什么：
  * cell{key, value, index(hidden)}
* 再注意，多加结构的时候，必须用cell来做一个单位，会让思路更简单，比如说这道题如果用treeSet
  * map(key, <mark style="color:red;">cell</mark>) && container(<mark style="color:red;">cell</mark>)
  * 并不能用<mark style="color:yellow;">map(key, index)</mark> && container(cell) , and <mark style="color:yellow;">Cell only have{key, index} ，why???</mark>





## Method 1

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

Method 2

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

