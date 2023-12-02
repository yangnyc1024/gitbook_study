# Problem 4 Permutation II with duplication

### Method 1: Swap- Swap(只对permutation有效)



弄清楚到底哪里重复：总的元素种类与个数相同，那么如果你固定过的元素值一样的话，剩下的元素的种类与个数一定也一样



<mark style="color:red;">重点在哪里？</mark>

* <mark style="color:blue;">duplication point 1:纵着看（swap-swap自动避免）</mark>
  * <mark style="color:red;">不同层之间，同一个元素（index相同的元素）只能被固定一次</mark>
* <mark style="color:blue;">duplication point 2:横着看</mark>
  * <mark style="color:red;">同一层上，对于要固定到同一个位置的两个元素value不能重复</mark>

<mark style="color:purple;">吃吐守恒定律，是对什么样的元素进行吃吐？</mark>

* <mark style="color:purple;">一定是不同层之间的元素</mark>

<mark style="color:purple;">既然是对同一层的去重？</mark>

* <mark style="color:purple;">去重的set需要加在每一层</mark>

```java
public List<List<Integer>> permutation(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null || nums.length == 0) {
        return result;
    }
    backTracking(result, nums, 0);
    return result;
}

// level: index: 当前层我正要固定index
// [0, index - 1]已经固定好的元素，不能用
// [index, nums.length - 1] 可以用来被固定到当前位置的元素

private void backTracking(List<List<Integer>> result, int[] nums, int level) {
    if (level == nums.length) {
        List<Integer> current = new ArrayList<>();
        for (int num: nums) {
            current.add(num);
        }
        result.add(current);
        return;
    }
    // 纵向上自动避免重复(swap - swap)
    // 横向上需要我们自己去重
    Set<Integer> valueHasBeenFixedInThisLevel = new HashSet<>();
    
    for (int i = level; i < nums.length; i++) {
        if (!valueHasBeenFixedInThisLevel.contains(nums[i])) {
            valueHasBeenFixedInThisLevel.add(nums[i]);
            swap(nums, i, level);
            backTracking(result, nums, level + 1);
            swap(nums, i, level);
        }
        //valueHasBeenFixedInThisLevel.remove(nums[i]); //不能吐，这是同一层，不需要吃吐
    }
}

private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
```

思考:

* &#x20;if (set.add(..)) vs  是否contains再add？前面可以简单



### Method 2 一个个加，怎么把横纵都去重



```java
public List<List<Integer>> permutation(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null || nums.length == 0) {
        return result;
    }
    
    //纵向去重
    Set<Integer> dedupIndexOnVerticallySet = new HashSet<>();
    List<Integer> current = new ArrayList<>();
    backTracking(result, nums, current, 0, dedupIndexOnVerticallySet);
    return result;
}

private backTracking(List<List<Integer>> result, int[] nums, List<Integer> current, int index, Set<Integer> dedupIndexOnVerticallySet) {
    // base case
    if (index == nums.length) {
        result.add(new ArrayList<>(current));
    }
    
    // current
    Set<Integer> dedupVallueOnHorizontallySet = new HashSet<>();
    // recursive rule
    for (int i = index; i < nums.length; i++) {
        if (!dedupIndexOnVerticallySet.contains(i)) { //注意这里是index！！！！
            if (!dedupValueOnHorizontallySet.contains(nums[i])) {
                dedupIndexOnVerticallySet.add(i);
                dedupValueOnHorizontallySet.add(nums[i]);
                current.add(nums[i]);
                backTracking(result, nums, current, index + 1,  dedupIndexOnVerticallySet);
                current.remove(current.size() - 1);
                dedupIndexOnVerticallySet.remove(i);
            }
        } 
    }
}
```

