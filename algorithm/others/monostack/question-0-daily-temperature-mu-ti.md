---
description: https://leetcode.com/problems/daily-temperatures/solutions/
---

# Question 0 Daily Temperature母体

### Summary

* 找右边，第一天比今天温度大的

### Method 1 暴力解&#x20;

* O(n^2)



### Method 2 Optimization

Step 1: 确认Use Case of Mono -Stack

Step 2: 用的是什么栈：动手过个例子（2元素就够了）

* 73遇到74置换==》用一个递减系
  * 因为留在stack里面是不符合条件的。。。，所以你既然要找更大的，留下的一定是更小的。
  * 然后当你踢到最后不能踢了，说明你找到这个踢的这个人的更大一个的元素
* 73遇到73置换么？==》单调非递增栈
  * 所以遇到自己相同的，是不符合条件的，也就是留在栈里面

Step 3: 栈里存的是什么物理意义

* value or index
* 人间题目问的是等几天，所以存的是index

```java
// Some code
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        // sanity check
        int[] result = new int[temperatures.length];
        Deque<Integer> monoStack = new ArrayDeque<>();
        for (int i = 0; i < temperatures.length; i++) {
            int curTemp = temperatures[i];
            while (!monoStack.isEmpty() && temperatures[monoStack.peekLast()] < curTemp) {
                int index = monoStack.pollLast();
                result[index] = i - index; // 谁置换你的，谁就是你的结果，被置换的人结果确定
            }
            monoStack.offerLast(i); //新来的一定要进栈，很容易忘（因为你需要看下能不能找到）
        }
        return result;
    }   
}
```

