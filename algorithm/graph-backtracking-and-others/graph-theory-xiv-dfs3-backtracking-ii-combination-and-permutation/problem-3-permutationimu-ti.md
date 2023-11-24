# Problem 3 Permutation I母题

#### Method 1 (只对combination有效)不能不加，只能加，一个一个加

High Level

* 什么是一个解？一个permutation
* 如何构造一个解？
  * 每一层：加一个元素进来
  * 分支：这一层所有可以加的元素中，你加谁呀？
  * 在哪收集解（对比subset）：所有元素都contains进来才行

注意

* All Path problem里，我们不允许同一个node在同一个path上使用多次，但是我们允许同一个node在不同path上使用多次
* Q我怎么知道我加这个元素没有？

**Implement 1**

TC& SC: O(n! \* n), O(n)

```java
public List<List<Integer>> permutation(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null || nums.length == 0) {
        return result;
    }
    List<Integer> current = new ArrayList<>();
    backTracking(result, nums, current, 0);
    return result;
}
// index：当前层我要固定的位置是谁：层数的信息
private void backTracking(List<List<Integer>> result, int[] nums, List<Integer> current, int index) {
    if (index == nums.length) {
        result.add(new ArrayList<>(current));
        return;
    }
    for (int i = 0; i < nums.length; i++) {
        // method 1: O(n) time to check current 里面是不是有nums[i], list: contains(val), O(n)
        if (!current.contains(nums[i])) {
            current.add(nums[i]);
            backTracking(result, nums, current, index + 1);
            current.remove(current.size() - 1);
        }
    }
}
```



**Implement 2**

**Use Case:**

* 我想知道某一个Character我在之前加过没加过==> loop up operation ==> set
* Set\<Integer> elementAddedSoFarInPreviousLevel
* 注意，这是对不同层之间纵向的去重，所以应该在不同层之间传递，一定是在主函数创建

这个代码可以跑过所有的test case，但是稳挂，<mark style="color:orange;">因为这个没办法对付去重？？</mark>

```java
public List<List<Integer>> permutation(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null || nums.length == 0) {
        return result;
    }
    Set<Character> elementAddedSoFar = new HashSet<>();
    List<Integer> current = new ArrayList<>();
    backTracking(result, nums, current, 0, elementAddedSoFar);
    return result;
}

// index:当前层我要固定的位置是谁：层数的信息
private void backTracking(List<List<Integer>> result, int[] nums, List<List<Integer>> current, int index, Set<Character> elementAddedSoFar) {
    if (index == nums.length) {
        result.add(new ArrayList<>(current));
        return;
    }
    for (int i = 0; i < nums.length; i++) {
        // method 2: O(n) space to check if previous level already used this character
        if (!elementAddedSoFar.contains(nums[i])) {
            elementAddSoFar.add(nums[i]);
            current.add(nums[i]);
            backTracking(result, nums, current, index + 1, elementAddSoFar);
            elementAddSoFar.remove(nums[i]);
            current.remove(current.size() - 1);
        }
    }
}
```

* 不同层之间的重复是 同一条path <mark style="color:blue;">同样index上的元素不能用多次</mark> vs ~~同样value的元素不能用多次~~
* 这道题之所以能过是因为这道题没有重复所有才能过，但是意义是不对的，要是有重复元素就错了

```java
public List<List<Integer>> permutation(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null || nums.length == 0) {
        return result;
    }
    
//注意这里！！！！！！！！！不是element，而是用index
    Set<Character> indexAddedSoFar = new HashSet<>();
    List<Integer> current = new ArrayList<>();
    backTracking(result, nums, current, 0, indexAddedSoFar);
    return result;
}

// index:当前层我要固定的位置是谁：层数的信息
private void backTracking(List<List<Integer>> result, int[] nums, List<List<Integer>> current, int index, Set<Character> indexAddedSoFar) {
    if (index == nums.length) {
        result.add(new ArrayList<>(current));
        return;
    }
    for (int i = 0; i < nums.length; i++) {
        // method 2: O(n) space to check if previous level already used this character
        if (!indexAddedSoFar.contains(i)) {
            indexAddedSoFar.add(i);
            current.add(nums[i]);
            backTracking(result, nums, current, index + 1, indexAddedSoFar);
            indexAddedSoFar.remove(i);
            current.remove(current.size() - 1);
        }
    }
}
```

#### Method 2 swap swap







**List Version**





**String Version**

```java
public class Solution {
   public List<String> permutations(String input) {
      // initial the return
     List<String> ret = new ArrayList<String>();
     // transfer input to a curChar
     char[] curChar = input.toCharArray();
    
     // curLevel: the String position
     dfsHelper(0, ret, curChar);
     return ret;
 
   }
 // dfsHelper(curLevel, ret, curChar)
   // corner case
         //if  curLevel reaches the curChar length
         // ret.add(curChar change to the )
         // return
    // iterate the possible position: from curLevel to the curChar.length
       // swap (possiblePostion, curLevel, curChar)
       // dfsHelper(curLevel, ret, curChar)
       // swap (possiblePostion, curLevel, curChar)
   private void dfsHelper(int curLevel, List<String> ret, char[] curChar) {
     if (curLevel == curChar.length) {
       ret.add(new String(curChar));
       return;
     }
     for (int possiblePosition = curLevel; possiblePosition < curChar.length; possiblePosition++) {
       swap(possiblePosition, curLevel, curChar);
       dfsHelper(curLevel + 1, ret , curChar);
       swap(curLevel, possiblePosition, curChar);
     }
   }
   private void swap(int a, int b, char[] curChar) {
     char temp = curChar[a];
     curChar[a] = curChar[b];
     curChar[b] = temp;
   }
  }
 
// TC O(n!)
// SC O(n)
```
