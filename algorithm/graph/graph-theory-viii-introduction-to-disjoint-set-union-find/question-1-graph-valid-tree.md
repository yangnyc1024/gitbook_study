# Question 1: Graph Valid Tree

#### 考

看到这句话要注意！You have a graph of N nodes labeled from 0 to n-1

* mark visited 可以用数组
* UF实现会比较简单



#### Method 1 DFS or BFS

* Tree and Graph的本质区别
* E是否等于V - 1
* 有没有环
* 有没有可能有一个点有两个爸爸



#### Method 2: Union Find

* 三个条件不变
* <mark style="color:red;">用UnionFind如何判断环的存在</mark>
  * 在你Union的时候，我要union的两个兄弟其实已经属于同一个帮派里的两个兄弟
  * （相连就是帮派，在一个帮派里等同于他们相连，所以再发现还可以相连，说明有环）



```java
class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (edges.length != n -1) {
            return false;
        }
        int[] laoda = int[n];
        for (int i = 0; i < n; i++) {
            laoda[i] = i;
        }
        for (int[] edge: edges) {
            int a = edge[0];
            int b = edge[1];
            int alaoda = find(a, laoda);
            int blaoda = find(b, laoda);
            if (alaoda == blaoda) {
                return false;
            }
            laoda[alaoda] = blaoda;            
        }
        return true;
    }
    
    private int find(int a, int[] laoda) {
        return laoda[a] = a == laoda[a] ? a: find(laoda[a], laoda);
    }
}
```
