---
description: Implementation
---

# Implementation

## Implementation of Prim's Algorithm



### Method 1: 朴素法

getUsedInput() is a magic function that get user input for what we need!

```java
int N = getUserInput();
int[][] graph = getUserInput();
int[] dist = new int[N + 1];
int[] visited = new int[N + 1];



// 习惯是如果不存在就return INF, main函数里调用prim的时候要检查return得结果，是不是INF
public int prim() {
    Arrays.fill(dist, Integer.MAX_VALUE);
    int result = 0;
    
    for (int i = 0; i < N; i++) {
        //找出一个距离现在集合最近的点，这个是算法的核心部分，而不是找的是原点最近的点
        int target = -1;
        for (int j = 1; j <= N; j++) {
            if (!visited[j] && (target == -1 || dist[target] > dist[j])) {
                target= j;
            }
        }
    }

    return result; // 注意如果有点不联通则不存在最小生成树
}
```





### Method 2: 堆化实现







## Implementation of Kuruska Algorithm

