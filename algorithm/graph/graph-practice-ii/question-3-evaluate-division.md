# Question 3 Evaluate Division

<mark style="color:orange;">注意这道题是多个query查询的问题</mark>

* 每个来做，可能有重复运算，之后可以用flow，类dp的算法？

## High Level

* it is a graph problem,&#x20;
  * vertex: different character,&#x20;
  * edge: equation for different character
  * undirected graph
* this is a reachable graph problem + calculate the weight
* dfs/ bfs to solve it

## Middle Level







```java

public double[] calEquation(List<List<String>> equations, double[] values, List<Liust<String>> queries) {
    // assume the input are valid
    
    double[] result = new double[queries.size()];
    
    // build Graph
    Map<String, Map<String, Double>> graph = buildGrpah(equations);
    
    int index = 0;
    for (List<String> query: queries) {
        Set<String> visited = new HashSet<>();
        String u = query.get(0);
        String v = query.get(1);
        if (u.equals(v)) { // 面试里不一定需要做检查，注意CART
            if (!graph.containsKey(u) || !graph.containsKey(v)) {
                result[index] = -1.0;
                index++;
            }else{
                result[index] = 1.0;
                index++;
            }
            continue;
        }
        result[index] = dfs(graph, visited, u, v, 1.0);
        result2[index] = bfs(graph, visited, u, v, 1.0);
        index++;
    }
    return result;
}
// return value的意义：目的是为了减脂6，
// 有结果，不应该是-1， 不然到不了（算不出来）结果应该是-1
// u 相当于current Node，
// v 相当于target Node
private double dfs(Map<String, Map<String, Double>> graph, Set<String> visited, String u, String v, double result) {
    if (u.equals(v)) {
        return result;
    }
    visited.add(result);
    Map<String, Double> neis = graph.get(u);
    if (neis != null) {
        for (String key: neis.keySet()) {
            if (!visited.contains(key)) {
                double result = dfs(graph, visited, key, v, result * neis.get(key));
                if (result != -1.0) {
                    return result;
                }
            }
        }
    }
}


private double bfs(Map<String, Map<String, Double>> graph, Set<String> visited, String u, String v, double result) {
    Deque<Pair> queue = new ArrayDeque<>();
    Pair root = new Pari(u result);
    queue.offer(root);
    visited.add(root);
    while(!queue.isEmpty()) {
        Pari current = queue.poll();
        Map<String, Double> neis = graph.get(current.cur);
        if (neis != null) {
            for (String nei: neis.keySet()) {
                double newResult = current.result * neis.get(nei);
                if (nei.equals(v)){
                    return newResult;
                }
                Pair new Pair = new Pari(nei, newResult);
                if(visited.add(neiPair)) {
                    queue.offer(neiPair);
                }
            
            }
        }
    }
    return -1.0;
}

private Map<String, Map<String, Double>> buildGraph(List<List<String>> equations, doubles[] values) {
    Map<String, Map<String, Double>> graph = new HashMap<>();
    for (int i = 0; i < equations.size(); i++) {
        double value = values[i];
        List<String> nodePair = equations.get(i);
        graph.putIfAbsent(nodePari.get(0), new HashMap<>());
        graph.putIfAbsent(nodePari.get(1), new HashMap<>());
        graph.get(nodePair.get(0)).put(nodePair.get(1), value);
        graph.get(nodePair.get(1)).put(nodePair.get(0), 1 / value);
    }
    return graph;
}




class Pair{
    String cur;
    double result;
    public Pair(String cur, double result) {
        this.cur = cur;
        this.result = result;
    }
    @Override
    public boolean equals(Object obj) {
        if(obj == this) return true;
        if (!obj instanceof Pair) return false;
        Pair temp = (Pair) obj;
        return this.cur.equals(temp.cur) && this.result == temp.result;
    }
    @Override
    public int hashcode(Object obj) {
        return (int) this.result * 31 + this.cur.length() *31 *31;
    }
}
```



following up question:&#x20;

* you may assume that evaluating the queries will not result in division by zero and
* what if there may exist contradictions, could you determine if there exist any contradictions? if yes return true otherwise return false







还是一个图问题，其实还是个reachable连通性的问题，不过什么叫做有contradictions，就是会不会存在另外一个方式到达一个点使得方式得到的result不同

* 我们的目的是寻求从start到target得reachable的方式
* 我们知道应有的结果，
  * 结果精度：Java/JavaScript，double判断，range：0.001 ==》 CART
  * 存不存在一个使得到达以后计算出的result和原始给定的，中途计算的





```java

public boolean checkIfContainsContradictions(List<List<String>> equations, double[] values) {
    Set<String> allNodes = new HashSet<>();
    Map<String, Double> visited = new HashMap<>();
    Map<String, List<Pair>> graph = buildGraph(equations, values);
    
    // 不联通图里的联通分量遍历的要点，从所有没有出发过的点出发一次
    // DFS return value represent contradictions
    for (String node: nodes) {
        for (String node: nodes) {
            if (!visited.containsKey(node) & dfs(graph, visited, node, 1.0)) {
                return true;
            }
        }
        return false;
    }
    
}
private boolean dfs(Map<String List<Pair>> graph, Map<String, Double> visited, String curNode, double val) {
    if (visited.containsKey(curNode)) {
        return Math.abs(visited.get(curNode) - val) >= ERRRANGE;
    }
    visited.put(curNode, val);
    for (Pair nei: graph.getOrDefault(curNode, new ArrayList<>())) {
        if (dfs(graph, visited, nei.cur, val * nei.result)) {
            return true;
        }
    }
    return false;
}

private Map<String, List<Pair>> buildGraph(List<List<String>> equations, doubles[] values) {
    Map<String, Map<String, Double>> adjList = new HashMap<>();
    for (int i = 0; i < equations.size(); i++) {
        double value = values[i];
        List<String> nodePair = equations.get(i);
        graph.putIfAbsent(nodePari.get(0), new HashMap<>());
        graph.putIfAbsent(nodePari.get(1), new HashMap<>());
        graph.get(nodePair.get(0)).put(new Pair(nodePair.get(1), value);
        graph.get(nodePair.get(1)).put(new Pair(nodePair.get(0), 1 / value);
    }
    return adjList;
}




class Pair{
    String cur;
    double result;
    public Pair(String cur, double result) {
        this.cur = cur;
        this.result = result;
    }
    @Override
    public boolean equals(Object obj) {
        if(obj == this) return true;
        if (!obj instanceof Pair) return false;
        Pair temp = (Pair) obj;
        return this.cur.equals(temp.cur) && this.result == temp.result;
    }
    @Override
    public int hashcode(Object obj) {
        return (int) this.result * 31 + this.cur.length() *31 *31;
    }
}
```
