---
description: coins
---

# Combination of coins

#### Method 2

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





#### TC& SC&#x20;

实际上M1和M2都是在对25a + 10b + 5c + d = 99求解，只是具体的实现不一样

* 所以这几种算法都是在尝试a\&b\&c\&d的所有可能性
* 所以这两种做法的复杂度是一样的
* 从减值的角度看，两种做法都在cur\_sum超过target就行了剪枝，是一样优秀的



#### Following Up question

Question: Given a set of n integers, divide the set into two subsets of n/2 size each such that the difference of the sum of two subsets is as minimum as possible. Return the minium difference(absolute value)

脱马甲的方式：把你构建的解的方式说出来：以加为不加：要么XXXX，要么XXXX

High Level + Recursion Tree:把每个元素分到两个subset里去，对于每个元素来说，要么去A，要么去B

tips

* 如果你知道total Sum，只记录A的Sum：BSum = totalSum - ASum
* Math.abs(total - Asum) - Asum) represent 两个subset. sum的差



```java
// Some code

public int mindifference(int[] array) {


}
```
