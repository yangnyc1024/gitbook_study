# Problem 1 Connecting Cities With Minimum cost



n个村庄，最小？

Step 1: 看出来是个最小生成树

Step 2: Apply Kruskal or Prims



```java
public int minimumCost(int n, int[][] connections) {
    intp[ laoda = new int[];
    for (int i = 0; i < n; i++) {
        laoda[i] = i;
    }
    Arrays.sort(connections, (a, b) -> Integer.compare(a[2], b[2]));
    int result = 0;
    int count = 0;
    
    for (int[] current : connections) {
        int a = current[0] - 1;
        int b = current[1] - 1;
        int alaoda = find(a, laoda);
        int blaoda = find(b, laoda);
        
        if (alaoda != blaoda) {
            result += current[2];
            count++;
            laoda[alaoda] = blaoda;
            if (count == n -1) {
                return result;
            }
        }
    }
    return -1;
}
private int find(int a, int[] laoda) {
    return laoda[a] = laoda[a] == a? a: find(laoda[a], laoda);
}
```
