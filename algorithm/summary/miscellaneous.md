---
description: Miscalleous
---

# Miscellaneous

Question：如何让java知道如何打印一个自己定义的class

Ans:必须要在class定义里override toString()

```python
Class A{
    int B;
    int C;
    int D;
    @Override
    public String toString(){
        return "" + B;
    }    
}
```





重复vs 必要

* 重复的一定没必要，没必要的不一定重复
* 永远都要有优化的心





Look Up Operation：我得知道我见没见过？遇见没有遇见过？

* 得知道这个字问题你算过没算过
* 要是知道算过了，得知道上次算他的结果是多少



什么是剪枝?

* 就是除去没必要的
* 能剪枝一定要剪枝



Question: queue 用哪组API

* 做题的角度，还是用offer，poll，peek
* 工作的时候用add，remove，element





<mark style="color:red;">PriorityQueue does not allow null elements</mark>





<mark style="color:red;">how to print int\[]\[]</mark>

```java
System.out.println(Arrays.deepToString(isPali));

```

parseInt

1. `parseInt(String s)`: Parses the `String` argument as a signed decimal integer.
2. `parseInt(String s, int radix)`: Parses the `String` argument as a signed integer in the specified radix (base).
