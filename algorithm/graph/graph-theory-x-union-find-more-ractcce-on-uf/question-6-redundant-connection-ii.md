# Question 6 Redundant Connection II

有向图还有可能因为没有环，但是有些有两个爸爸导致不合法



#### Method 1: DFS

*   有向图的root是谁呢？

    * tree里根节点是唯一的一个没有爸爸的点, indegree of root为0有没有可能找不到root，如果不存在入度为2的点呢？


* Question：有没有可能找不到root：如果不存在入度为2的点呢？（need复习）
*   不合法的情况到底有几种

    * every node has only one parent, and there is a Cycle that include the root node (cycle edge)
    * there is a node with two parents but no cycle (two-parent edge)
    * there is a node with two parents; also, there is a cycle! (环上最后一条边)

    <figure><img src="../../.gitbook/assets/Screenshot 2023-10-26 at 11.31.18 PM.png" alt="" width="177"><figcaption></figcaption></figure>

有向图找环

* 如果有环，那就从环上的点出发，找到环上的最后一条边
* 如果没有环，有个一点有两个parent

```java
private static final int UNIVISITED = 0;
private static final int VISITING = 1;
private static final int VISITED = 2;


//尽量不要用global变量
private Integer markNode = -1; //看看有没有入度为2的点
int[] possibleResult = new int[]{-1, -1}; 

public int[] findRedundantConnection(int[][] edges) {
    if (edges == null. || edges.length == 0) {
        return new int[]{-1, -1};
    }
    
    int[] indegree = new int[edges.length + 1];
    Map<Integer, Map<Integer, Integer>> graph = buildGraph(edges, indegree);
    int[] visited = new int[edges.length + 1]; 
    
     List<Integer> path = new ArrayList<>();
     int[] cycle = null;
     if (markNode != -1) {
         int startNode = -1;
         for (int i = 1; i < indgree.length; i++) {
             if (indegree[i] == 0) {
                 startNode = i;
             }
         }
         cycle = DFS(graph, startNode, visited, path);
     }  else {
         //当不存在indegree为2的点的时候，无法确定root
         for (int i = 1; i < edges.length; i++) {
             cycle = DFS(graph, visited,path);
             if (result != null) {
                 break;
             }
         };
     }
     if (cycle == null) {
         return possibleResult; //是一个怎么样的边？造成indegree为2的边
     } else {
         return cycle;
     }
}
private int[] findEdge(List<Integer> cycle, Map<Integer, Map<Integer, Map<Integer, Integer>>> graph) {
    int startNode = cycle.get(cycle.size() - 1);
    int[] result = new int[]{cycle.get(cycle.size() -2), cycle.get(cycle.size() - 1)};
    if (startNode.equals(markedNode)) {
        return result;
    }
    int index = cycle.size() - 2;
    while (index - 1 >= 0 && cycle.get(index) != startNode) {
        int u = cycle.get(index - 1);
        int v = cycle.get(index);
        if (v.equals(markNode)) {
            return new int[]{u, v};
        }
        if (graph.get(result[0]).get(result[1]) < graph.get(u).get(v)) {
            result[0] = u;
            result[1] = v;
        }
        index--;
    }
    return result;
}
private Map<Integer, Map<Integer, Integer>> = buildGraph(int[][] edges, int[] indegree) {
    Map<Integer, Map<Integer, Integer>> graph = new HashMap<>();
    
    for (int i = 0; i < edges.length; i++)  {
        int u = edges[i][0];
        int v = edges[i][1];
        indegree[v]++;
        if (indegree[v] == 2) {
            markNode = v;
        }
        graph.putIfAbsent(u, new HashMap<>());
        graph.get(u).put(v, i);
    }
    return graph;
}
```



#### Method 2

思路分析, Three case:

* Every node has only one parent, and there is a cycle which include root node
* There is a node with two parents, no cycle
* There is a node with two parents, and a cycle

Union 的过程中要能去区分：indegree = 2 的结果啊，还是环的结果呢？

Union(a,b)的时候，

* 如果alaoda = blaoda没问题，cycle造成的结果
* 如果alaoda != blaoda: 有没有可能是个possibleResult呢？

区别是什么？

* union(a,b)的时候b的老大是谁，因为我们union的顺序是b加入a的话，b的老大是不是自己

```java
public int[] findRedundantConnect(int[][] edges) {
    if (edges == null || edges.length == 0) {
        return new int[]{-1, -1};
    };
    int[] laoda = new int[edges.length + 1];
    int[] result1 = null;// indegree 为2造成的结果
    int[] reuslt2 = null; // cycle造成的结果
    for (int[] edge: edges) {
        int alaoda = find(edge[0], alaoda);
        int blaoda = find(edge[1], blaoda);
        if (blaoda != edge[1]) {
            result1 = edge;
        }else {
            laoda[blaoda] = alaoda;
        }
    }
    if (result1 == null) {
        return result2;
    }
    if (result2 == null) {
        return result1;
    }
    for (int[] edge: edges) {
        if (edge[1]== result1[1]) {
            return edge;
        }
    }
    return new int[0];
}
private int find(int a, int[] laoda) {
    return laoda[a] = laoda[a] == a? a: find(laoda[a], laoda);
}
```

&#x20;

为什么一定要遍历找result而不是直接return result1 和result2

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-03 at 5.17.28 PM.png" alt="" width="563"><figcaption></figcaption></figure>

