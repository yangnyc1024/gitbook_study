# HashMap API

#### API 1: put(K key, V value)

add new key-value pairs to the HashMap



#### API 2: clear()



#### API 3: containsKey(Object key)

check whether this map contains a mapping for the specified key



#### API 4: containsValue(Object value)





#### API 5: get(Object key)





#### API 6: getOrDefault(Object key, V defaultValue)



#### API 7: isEmpty()



#### API 8: putAll(Map\<? extends K, ? extends V> m)



#### API 9: putIfAbsent(K key, V value)



#### API 10: remove(Object key)



#### API 11: remove(Object key, Object value)



#### API 12: size()



#### API 13: keySet()

#### API 14: entrySet()



* 遍历map的一种方法

```java
for (Map.Entry<Integer, String> entry : map.entrySet())
```

#### API 14.1: getKey()



#### API 14:2 getValue()

####

#### API 15: values()

returns a Collection view of the values contained in this map

* 可以遍历values，但是不能找到对应的key

```java
Iterator<Map.Entry<Integer, String>> entryIter = map.entrySet().iterator();

while (entryIter.hasNext()) {
    Map.Entry...?
}
```



