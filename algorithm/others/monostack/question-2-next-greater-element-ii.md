# Question 2 Next Greater Element II

## Summary

* 顺时针找比他大的



### Method 1 Brute force

```java
// Some code

public int[] nextGreatElement(int[] sums) {
    int[] result = new int[sums.length];
    for (int i = 0; i < nums.length; i++) {
        result[i] = -1;
        for (int j = 1; j < nums.length; j++) {
            if (nums[(i + j) % array.length]) > nums[i] {
                result[i] = nums[(i + j) % array.length];
                break;
            }
        }
    }
    return result;
}
```

### Method 2 Optimization

* 如何在一个circular array里想apply一般的算法，又不升级时间维度，延长，卡sliding window size = length
* 如何让元素一个一个来，但是又不真的延长

```java
// Some code
for (int i = 0; i < array.length; i++) {
    System.out.println(array[i]);
}
for (int i = 0; i < 2*  array.length; i++) {
    System.out.println(array[i % array.length]);
}
```

```java
// Some code
public int[] nextGreatElement(int[] nums) {
    int[] result = new int[nums.length];
    Arrays.fill(result, Integer.MIN_VALUE);
    
    Deque<Integer> monoStack = new ArrayDeque<>();
    for (int i = 0; i < 2 * nums.length; i++) {
        while (!monoStack.isEmpty() && nums[monoStack.peekLast()] < nums[i % nums.length]) {
            result[monoStack.pollLast()] = nums[i % nums.length];
        }
        monoStack.offerLast(i % nums.length);
    }
    return result;
}
```

### Follow Up：如果我 不让你取mod怎么办？不让你延长怎么办？

Analysis

* Stack的特点，一堆元素都放进栈，会倒置（LIFO）
* 如果把元素都反向放进栈：从栈顶到栈尾就是原array的顺序
* Stack顶端元素物理意义：当前距离你来的元素右边最近的可能是第一个比大的元素是谁？
* 对于最后一个元素，他右边第一个比他大的，如果能靠前，就不要后面满足条件

Details

* Case 1: 新来的元素，如果栈顶元素已经大于它了，这个栈顶元素其实就是solution
* Case 2:新来的元素，如果栈顶元素已经小于它了，这个元素肯定不是新来元素（我）的解，那这个元素有没有可能是新来元素前面元素的解呢？ XXX不可能
  * 元素是倒着来的，对于lastElement前面的元素来说，lastElement比栈顶的元素离他们更近（因为如果连我都不如，我就可能是解啊）

```java
// Some code
public int[] nextElement(int[] nums){
    int[] result = new int[nums.length];
    Deque<Integer> stack = new ArrayDeque<>();
    // 倒着放元素
    for (int i = nums.length - 1; i >= 0; i--) {
        stack.offerLast(i);
    }
    // 倒着来元素
    for (int i = nums.length - 1; i >= 0; i--) {
        result[i] = -1;
        while (!stack.isEmpty() && nums[stack.peekLast()] <= nums[i]) {
            stack.pollLast();
        }
        if (!stack.isEmpty()) {
            result[i] = nums[stack.peekLast()];
        }
        stack.offerLast(i);
    }
    return result;
}
```

