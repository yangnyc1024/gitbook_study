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
