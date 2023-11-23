# Problem 3 Minimum time to finish all jobs

#### Method 1先做出来

```java
// Some code
public int minimumTimeRequire(int[] jobs, int k) {
    int[] result = {Integer.MAX_VALUE};
    int[] worker = new int[k];
    dfs(jobs, 0, result, worker, 0);
    return result[0];
}

private void dfs(int[] jobs, int index, int[] result, int[] worker, int max) {
    if (index == jobs.length) {
        result[0] = Math.min(result[0], max);
        return;
    }
    for (int i = 0; i < worker.length; i++) {
        worker[i] += job[index];
        dfs(jobs, index + 1, result, worker, Math.max(worker[i], max));
        worker[i] -= job[index];
    }
}

```





#### Method 2

```java
// Some code

public int minimumTimeRequire(int[] jobs, int k) {
    int[] result = {Integer.MAX_VALUE};
    int[] worker = new int[k];
    dfs(jobs, 0, result, worker, 0);
    return result[0];
}

private void dfs(int[] jobs, int index, int[] result, int[] worker, int max) {
    if (index == jobs.length) {
        result[0] = Math.min(result[0], max);
        return;
    }
    for (int i = 0; i < worker.length; i++) {
        worker[i] += job[index];
        dfs(jobs, index + 1, result, worker, Math.max(worker[i], max));
        worker[i] -= job[index];
    }
}
```
