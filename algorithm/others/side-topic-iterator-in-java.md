# Side Topic: Iterator in Java

#### Interface Iterator



#### Java 中常见的数据结构和它内置的iterator: create an instance o f iterator





#### Iterator 的subInterface







#### API 1: E next()

Returns the next element in the iteration

用法：iterator.next()

Example: ArrayList

Example: set

Example treeSet



#### API2: boolean hasNext()

Return true if the iteration has more elements

Example: ArrayList

Example: set

Example treeSet





思考：

* 判断还有没有下一个
* 真的拿出下一个
* 内部的use case：我需要给下一次遍历做好准备





#### API 3: void forEachRemaining (Consumer\<? super E> action)

Performs the given action for each remaining element until all elements has been processed or the action throws an exception





#### API 4 void remove()

Removes from the underlying colleciton the last element returneed by this iterator(optional operation)

