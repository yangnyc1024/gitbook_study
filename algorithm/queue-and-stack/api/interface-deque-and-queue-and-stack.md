# Interface Deque & Queue & Stack



A linear collection that supports element insertion and removal at both ends. The name deque is short for "double-ended queue" and is usually pronounced "deck"

* queue是更generate的interface

<figure><img src="../../.gitbook/assets/Screenshot 2023-09-16 at 1.39.10 PM.png" alt=""><figcaption></figcaption></figure>

| Type of Operation | First Element(throw exception) | First Element(Return null/ false)             | Last Element(throw expection) | Return speical value                         |   |
| ----------------- | ------------------------------ | --------------------------------------------- | ----------------------------- | -------------------------------------------- | - |
| Insert            | addFirst(e)                    | <mark style="color:red;">offerFirst(e)</mark> | addLast(e)                    | <mark style="color:red;">offerLast(e)</mark> |   |
| Remove            | removeFirst()                  | <mark style="color:red;">pollFirst()</mark>   | removeLast()                  | <mark style="color:red;">pollLast()</mark>   |   |
| Examine           | getFirst()                     | <mark style="color:red;">peekFirst()</mark>   | getLast()                     | <mark style="color:red;">peekLast()</mark>   |   |



<figure><img src="../../.gitbook/assets/Screenshot 2023-09-16 at 1.44.29 PM.png" alt=""><figcaption></figcaption></figure>

* 这个是固定的！！！！
* 放是在last，拿是在first

| Queue     | Equivalent Deque Method |
| --------- | ----------------------- |
| add(e)    | addLast(e)              |
| offer(e)  | offerLast(e)            |
| remove()  | removeFirst()           |
| poll()    | pollFirst()             |
| element() | getFirst()              |
| peek()    | peekFirst()             |





<figure><img src="../../.gitbook/assets/Screenshot 2023-09-16 at 1.45.57 PM.png" alt=""><figcaption></figcaption></figure>

* stack只对first

| Stack Method | Equivalent Deque Mathod |
| ------------ | ----------------------- |
| push(e)      | offerFirst(e)           |
| pop()        | pollFirst()             |
| peek()       | peekFirst()             |



## Summary&#x20;

| 概念区分（逻辑层面）  | 内存里的存放方法           | 对应的java class          | 对应的java interface |
| ----------- | ------------------ | ---------------------- | ----------------- |
| queue(FIFO) | array/ linked list | ArrayDeque/ LinkedList | Queue             |
| stack(LIFO) | array/ linked list | ArrayDeque/ LinkedList | Deque             |
| deque       | array/ linked list | ArrayDeque/ LinkedList | Deque             |
