# Question 2 Number of Island II



#### Method 1:  Brute Force(dfs)

for each position: add

#### Method 2

Why is a use case for Union Find?

* 动态图问题：每一次都加入一个新的点

Step 1: 思考时是不是Union Find的Use case: Yes

Step 1.5: Union Find开多长

* 长度m\* n
* 即便是没有给Board也要自己记录Board为什么？
* 为了union的时候知道邻居是不是1

Step 2:思考要union什么

* 上下左右四个方向1
* 周围的1一定有老大(一定是一个联通分量了)
* <mark style="color:purple;">一个一个operation，一个个query，一个个position(防止重复，防止超界invalid)</mark>
* detail
  * 我们的result从何而来？result是每一次有多少个联通分量，一开始这个图里其实全是0(水)，一开始的count= 0;
  * 一般来说，union只能让count变得更少，在哪家这个count呢？每次来一个点，我们就直接默认他自己租整了一个单独的岛，如果他能union别人，union里会吧count减到正常值。





```java

public List<Integer> numIsland2(int m, int n, int[][] positions) {
    int[][] graph = new int[m][n];
    List<Integer> result = new ArrayList<>();
    UF uf = new UF(m * n);
    for (int[] position : positions) {
        int x = position[0];
        int y = position[1];
        if (graph[x][y] == 1) {
            result.add(uf.count);
            continue;
        }
        graph[x][y] = 1;
        uf.count++;
        for (int[] dir: dirs) {
            int neiX = x + dir[0];
            int neiY = y + dir[1];
            if (isValid(graph, neiX, neiY) && graph[neiX][neiY] == 1) {
                uf.union(x * n + y, neiX* n +neiY);
            }
        }
        return result;
    }
}

class UF{
    int[] laoda;
    int count;
    public UF(int n) {
        this.laoda = new int[n];
        for (int i = 0; i < n; i++) {
            laoda[i] = i;
        }
        this.count = 0; ///注意这个0
    }
    public void union(int a, int b) {
        int alaoda = find(a);
        int blaoda = find(b);
        if (alaoda != blaoda) {
            laoda[alaoda] = blaoda;
            count--; //注意这里
        }
    }
    public int find(int a) {
        return laoda[a] = laoda[a] == a? a: find(laoda[a]);
    }
}
```

这个方法快在哪？为什么动态图就这么快？

* 对于每一次的变化
* dfs: 变了我重来一次，刚才算过我再算一次
* uf：对于变化的部分union起来，以前算过的仍然存在
