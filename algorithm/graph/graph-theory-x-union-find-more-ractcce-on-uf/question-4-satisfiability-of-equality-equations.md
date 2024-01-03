# Question 4 Satisfiability of Equality Equations

hint1: What actually is this problem?

* 这是一个图问题
* 点：a.b...c....d.z.
* 边：a= b

这个问题是你构建的图论中什么问题？

能不能找到一组值使得所有的equation都成立

* 存不存在一组不想等(不同属)的两个点但是却出现在同一个联通分量里



#### Method Union Find

```java
public boolean equationPossible(String[] equations) {
    int[] laoda = new int[26];
    for (int i =0; i < 26; i++) {
        laoda[i] = i;
    }
    // "a==b"
    for (String equation: equations) {
        if (equation.charAt(1) == '=') {
            int alaoda = find(laoda, equation.charAt(0) - 'a');
            int blaoda = find(laoda, equation.charAt(3) - 'a');
            if (alaoda != blaoda) {
                laoda[alaoda] = blaoda;
            }
        }
    }
    for (String equation: equations) {
        if (equation.charAt(1) == '!') {
            int alaoda = find(laoda, equation.charAt(0) - 'a');
            int blaoda = find(laoda, equation.charAt(3) - 'a');
            if (alaoda != blaoda) {
                return false;
            }
        }   
    }
}
private int find(int[] laoda, int a) {
    return laoda[a] = laoda[a] == a? a: find(laoda, laoda[a]);
}
```
