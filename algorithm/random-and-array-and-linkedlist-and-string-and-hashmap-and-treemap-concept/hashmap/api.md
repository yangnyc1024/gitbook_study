# API



## API 14: entrySet()



* 遍历map的一种方法

```java
for (Map.Entry<Integer, String> entry : map.entrySet())
```

## API 15: values()

* 可以遍历values，但是不能找到对应的key

```java
Iterator<Map.Entry<Integer, String>> entryIter = map.entrySet().iterator();

while (entryIter.hasNext()) {
    Map.Entry...?
}
```



