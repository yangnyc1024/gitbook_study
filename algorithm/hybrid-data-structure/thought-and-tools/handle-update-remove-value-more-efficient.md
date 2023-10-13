# Handle update/remove value more efficient

Method 1: Lazy deletion:

* lazily remove the value(mark the value as delete but not really remove it, remove it only when it is at the top of the heap)
* Implement:&#x20;
  * hashMap?
  * Element with boolean isDelete?

Method 2:&#x20;

* We should maintain the mapping of the value with its position(index)
* Implement: HashMap?

Method 3:

* consider alternatives, such as TreeMap/ TreeSet

