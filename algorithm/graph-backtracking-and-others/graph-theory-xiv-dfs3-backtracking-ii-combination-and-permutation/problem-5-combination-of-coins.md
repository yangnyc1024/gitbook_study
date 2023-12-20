# Problem 5 Combination of coins

### Method 1一个一个加

* each level: 每一层我只拿一个硬币
* each branch: 可以选择的硬币&确保不会超过&确保选的是比之前的小

<pre class="language-java"><code class="lang-java">public List&#x3C;List&#x3C;Integer>> combinations(int target, int[] coins) {
    // sanity check
    // initial 
    List&#x3C;List&#x3C;Integer>> result = new ArrayList&#x3C;>();
    if (coins == null || coins.length == 0) {
        return result;
    }
    int[] path = new int[coins.length]; // 因为你需要记录一共这个元素用了多少次，所以需要对该类型的coin进行记录
    // dfs
    backTracking(result, path, coins, target, 0);
    // return
    return result;
<strong>}
</strong><strong>
</strong><strong>private void backTracking(List&#x3C;List&#x3C;Integer>> result, int[] path, int[] coins, int target, int index) {
</strong><strong>    // base case
</strong><strong>    if (target == 0) {
</strong><strong>        addCurrentResult(result, path);
</strong><strong>        return;
</strong><strong>    }            
</strong><strong>    
</strong><strong>    // dfs , i代表你拿了谁
</strong><strong>    for (int i = index; i &#x3C; coins.length; i++) {
</strong><strong>        if (target - coins[i] >= 0) {
</strong><strong>            path[i] += 1;
</strong><strong>            backTracking(result, path, coins, target - coins[i], i);
</strong><strong>            path[i] -= 1;
</strong><strong>        }
</strong><strong>    }
</strong><strong>    
</strong><strong>    // 
</strong><strong>}
</strong></code></pre>

#### Master alter method:

```
// Some code
```

### Method 2考虑数量

```java
public List<List<Integer>> combinations(int target, int[] coins) {
    List<List<Integer>> result = new ArrayList<>();
    if (coins == null || coins.length == 0) {
        return result;
    }
    List<Integer> current = new ArrayList<>();
    backTracking(result, current, coins, target, 0)l
    return result;
}

// index:当前层正在考虑哪种硬币：coins[index]这种
private void backTracking(List<List<Integer>> result, List<Integer> current, int[] coins,int target, int index) {
    if (index == coins.length) {
        if (target == 0) {
            result.add(new ArrayList<>(current));
        }
        return;
    }
    // 对于当前层你正在考虑的这种硬币coins[index]你最多拿多少个
    int maxNumberUCanTake = target/coins[index];
    
    // 分支：这种硬币你拿几个 range: [0, maxNumberUCanTake]
    for(int howManyDidUTake = 0; howManyDidUTake <= maxNumberUCantake; howManyDidUTake++) {
        current.add(howManyDidUTake);
        backTracking(result, current,coins, target - howManyDidUTake * coins[index], index + 1);
        current.remove(current.size() - 1);
    }
}
```

* 如果用list或者StringBuilder，这里是append不是同一个index赋值操作，所以不能忘记吃吐

老一辈艺术家的写法

```java
// Some code
```



#### TC& SC&#x20;

实际上M1和M2都是在对25a + 10b + 5c + d = 99求解，只是具体的实现不一样

* 所以这几种算法都是在尝试a\&b\&c\&d的所有可能性
* 所以这两种做法的复杂度是一样的
* 从减值的角度看，两种做法都在cur\_sum超过target就行了剪枝，是一样优秀的



####
