---
description: https://leetcode.com/problems/valid-triangle-number/description/
---

# Question Valid Triangle Number



#### 理解题目

* 什么是三角形，任意两条边的和大于第三条边
*

#### Method 1

最笨的方法是枚举所有可能的三边组合，那么什么叫找基准点：

* 固定基准点为任意条边
* 我想知道有多少对双边之和大于我fix的这条边，two sum

Logic

* for every possible fixed edge, we want to know how many pairs of sum > target
* this is a two sum problem

Detail Logic

* sort the array
* 注意问题的不同，how many pairs >/>= / <= target  VS  how many pairs = target





```java
// Some code


public int triangleNumber(int[] nums) {
    if (nums == null || nums.length < 3) {
        return 0;
    }
    Arrays.sort(nums);
    int count = 0;
    for (int largeEdgeIndex = 2; largeEdgeIndex < nums.length; largeEdgeIndex++) { //固定的边是最长的longest Edge
        count += sumLargerThan(nums, nums[i], 0, largeEdgeIndex - 1); // 你要找的点是在这个最大边之前
    }
    return count;
}
private int sumLargerThan(int[] nums, int target, int left, int right) {
    int count = 0;
    while (left < right) {
        int curSum = nums[left] + nums[right];
        if (curSum < target){
            left++;
        } else {
            count += (right - left);
            right --;
        }
    }
    return count;
}
```
