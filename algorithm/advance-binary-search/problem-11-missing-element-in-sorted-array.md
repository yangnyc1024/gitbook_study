# Problem 11 Missing Element in Sorted Array





Method 1: brute force



Method 2: Binary Search

* Find first occurrence of already missing >= K
* Find last Occurrence of already missing < K

加入我就是要找 last occurrence of already missing < K

* 到last occurence 已经missing了多少个：
  * already missing = array\[last\_occurence]- last\_occurence - array\[0]
* 到last occurrence还有几个没有missing
  * K already missing
* 最终第k个missing的数字
  * result = array\[last\_occurence] + 到last occurrence还有几个没missing
    * \= array\[last\_occurence] + K-already missing
    * \= array\[last\_occurence] + K + (array\[last\_occurence] - last\_occurrence - array\[0])
    * \= K+ last\_occurence + array\[0]

```java
```

