# Question 6 Longest Increasing Subsequence

#### Method 1暴力解(从后往前，但是不会用在面试中，只是为了训练)

```java
public int longest(int[] array) {
    // assume array valid
    int[] longest = new int[]{1};
    int currentLength = 0;
    dfs(longest, currentLength, array, array.length - 1, null);
    return longest[0];
}
private void DFS(int[] longest, int currentLength, int[] array, int index, Integer lastAddedValue) {
    // 哪里都是解
    longest[0] = Math.max(longest[0], currentLength);
    
    // branch 所有在index之前比加过的第一个元素还要小的元素，我要知道上次加了谁？
    for (int i = index; i >= 0; i++) {
        if (lastAddedValue == null || array[i] < lastAddedValue) {
            dfs(longest, currentLength + 1, array, array.length - 1, array[i]);
        }
    }
}
```

从所有解的角度来衡量：dfs走的每一条路都是不一样，没有任何了一步计算的path

只说剪枝（我这啊哦这条路最终的答案肯定是不hi我要的，那我就压根不去）

去重：我这条路以前已经走过了，答案我知道了，现在不想再走一遍了



#### Method 2 从backtracking 到pure recursion

```java
public int pureRecursion(int[] array, int index) {
    if (index == array.length) {
        return 0;
    }
    int subproblemResult = 0;
    for (int i = index + 1; i < array.length; i++) {
        if (array[i] > array[index]) {
            subproblemResult = Math.max(subproblemResult, PureRecursion[i]);
        }
    }
    return subproblemResult + 1;
}
```

看到重复的input size recursion call

* 在1，2，3都调用了pureRecursion（array，4）input size一样，都是4
* 答案一定都是一样的==》产生了重复&没有必要的运算
* pure recursion里的input一样，结果一样，就是完全一样的问题



#### Method 3 从pure recursion to recursion memo

既然以某个index为开始的LIS一定永远都不会改变==》 那么我们以每一个starting index为开始的LIS只需要计算一次

```java
```

Longest Increating Subsequence时间复杂度是多少？O(N!)==> O(N^2)

#### Method 4真的确定有优化， pure recursion memo to dynamic programming

顺序又回到了ending index上：linear scan回头看
