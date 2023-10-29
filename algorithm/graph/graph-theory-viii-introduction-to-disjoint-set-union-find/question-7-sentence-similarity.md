---
description: Similarity
---

# Question 7 Sentence Similarity





#### Method 2 Union Find

* 问我们a和c是不是similar--》 a和c在不在一个group里
* 特殊之处：点如果是String的话，联通分量问题能不能用union find？可以的
* int\[] laoda ==>  Map\<String, String> laoda
  * key: word, value: word 所在的group的老大
* int\[] size ==> Map\<String, Integer> size
  * key: word, value: word所在的group的size

```java
// Some code
public boolean areSentecesSimilarTwo(String[] words1, String[] words2, List<List<Pari>> pair) {
    // uf
    Map<String, String> laoda = new HashMap<>();
    Map<String, String> size= new HashMap<>();
    for (List<String> pair: pairs) {
    
    }
}
//初始化 + find
private String find(Map<>???? Map<String, String> laoda, String a) {
    if (!laoda.containsKey(a)) {
        laoda.put(a,a);
        size.put(a, 1)
    }
    String zhenlaoda = a;
    while (!zhenlaoda.equals(laoda.get(zhenlaoda))) {
        zhenlaoda = laoda.get(zhenlaoda);
    }
    // path compression
    while (!a.equals.(laoda.get(a))) {
        String temp = laoda.get(a);
        laoda.put(a, zhenlaoda);
        a = temp;
    }
    return zhenlaoda;
}
```

