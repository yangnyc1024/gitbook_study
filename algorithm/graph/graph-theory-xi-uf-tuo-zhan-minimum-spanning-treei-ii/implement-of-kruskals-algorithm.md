---
description: Implement
---

# Implement of Kruskal's Algorithm

Step1: Sort all edges in increasing order of their edge weights

Step2: Pick the smallest edge

Step3: Check if the new edge creates a cycle or loop in a spanning tree/

Step4: If it does not form the cycle, then include that edge in MST. Otherwise, discard it.

Step5: Repreat from step 2 until it includes |V| - 1 edges in MST.

```java
int N = getUserInput(); // n Vertices
int M = getUserInput(); // m Edges
int[] laoda = new int[N];
Edge[] edges = new Edge[M];

class Edge implements Comparable<Edge> {
    int src;
    int dest;
    int weight;
    public edge(int src, int dest, int weight) {
        this.src = src;
        this.dest = dest;
        this.weight = weight;
    }
    @Override
    public int compareTo(Edge edge) {
        return Integer.compare(this.weight, edge.weight);
    }
}

private int find(int x) {
    return laoda[x] = laoda[x] == x? x: find(laoda[x]);
}


public int kruskal() {
    int MSTWeight = 0;
    int numberOfEdge = 0;
    Arrays.sort(edges);
    for (int i = 0; i < M; i++){
        Edge edge = edges[i];
        int a  = edge.src;
        int b = edge.dest;
        int weight = edge.weight;
        
        // 可以加union by weight at *
        int alaoda = find(a);
        int blaoda = find(b);
        if (alaoda != blaoda) {
            // *
            laoda[alaoda] = blaoda;
            MSTWeight += weight;
            numberOfEdge++;
            if (numberOfEdge == N - 1) {
                return MSTWeight;
            }
        }
    }
    if (numberOfEdge < N - 1) {
        return Integer.MAX_VALUE;
    }
    return MSTWeight;
}
```
