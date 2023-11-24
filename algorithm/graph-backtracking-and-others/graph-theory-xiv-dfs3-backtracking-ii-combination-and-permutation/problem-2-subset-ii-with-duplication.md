---
description: repeat
---

# Problem 2 Subset II with duplication

#### Method 1（每一层就是加不加，你只能加第一个）

这种去重问题其实本质上是backtracking里面的剪枝问题

* 不是先产生所有的解，再用set去重==》 思想错误
* <mark style="color:purple;">不产生重复的解，我知道重复我就不走</mark>



<mark style="color:blue;">Step 1：分析为什么会发生重复，画图</mark>



<mark style="color:blue;">Step 2：说出去重的方法</mark>

* 处理方法：二选一
* 也就是说，所有加的分支都照常不懂，加就是加，就正常加，但你要说不加那就再也不加了
* 那你怎么做到要不加后面再来的也不要了？<mark style="color:orange;">这个写法基于assumption：同样的元素都连在一起出现</mark>
  * <mark style="color:orange;">while (index + 1 < nums.length && nums\[index + 1] == nums\[index]) { index++;}</mark>
  * <mark style="color:red;">如果你没有了assumption，就必须需要先sort</mark>

List Version

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null || nums.length == 0) {
        return result;
    }
    Arrays.sort(nums);
    List<Integer> current = new ArrayList<>();
    backTracking(result, nums, current, 0);
    return result;
}
// index: 当前层我正要考虑的元素
private void backTracking(List<List<Integer>> result, int[] nums, List<Integer> current, int index) {
    if (index = nums.length) {
        result.add(new ArrayList<>(current));
        return;
    }
    // add
    current.add(nums[index]);
    backTracking(result, nums, current, index + 1);
    current.remove(current.size() - 1);
    
    // not add
    while (index + 1 < nums.length && nums[index + 1] == nums[index]) {
        index++;
    }
    backTracking(result, nums, current, index + 1);

}
```

String Version

```java
/*
Clarification:
 Input: a String set(String)
 Output: a List of String ret(List<String>)
 repeat!!! && no fix length output

High Level:
 combination problem ----- dfs backtracking ---- each step choose or not choose

Middle Level:
 Recursion tree example: "aab"
                        ""
                /                 \
              "a"                   ""          ----- level 1           
          /         \        /                \
        "aa"         "a"    "a"(not choose)    ""      ---- level 2         
     /     \        /     \
 "aab"      "aa"  "a"      ""                              ----- level 3

1) For each level, we decide if we choose a new element, for example level one, we decide to choose 'a' or not.
2) We do this recursively. It means based on level 1 result, for level 2, we decide to choose or not 'a', which is the second element in the oriString.
3) To avoid repetition, since 'a' is repeated, if we choose before, then we keep choosing it. If we don't choose it, we wont choose it.
4) When we iterate all the possible element we can choose, it means we reach oriString.length(), we output our result;


Induction Rule:
1) get level info from preLevel, base on oriString's char at this level, decide add or not add
2) dont forget backtracking.


Subproblem:
1) curLevel choose this element, add to curString, move to curLevel + 1, backtracking this element in
2) curLevel not choose this element, keep curString, move to curLevel + 1

Add Result:
1) curLevel reach the oriString's length + 1

Base case:
1) curLevel reach the oriString's length + 1

Key Parameter:
1) curLevel: the position we decide to choose or not choose from oriString

TC & SC: O(2^n), O(n)
*/


public class Solution {
 public List<String> subSets(String set) {
   // Write your solution here.
   List<String> ret = new ArrayList<>();
   if (set == null) return ret;
   StringBuilder curString = new StringBuilder();
   char[] oriString = set.toCharArray();
   Arrays.sort(oriString);
   helper(oriString, curString, ret, 0);

   return ret;
 }
 private void helper(char[] oriString, StringBuilder curString, List<String> ret, int curLevel) {
   if (curLevel == oriString.length) {
     ret.add(curString.toString());
     return;
   }   
   // add
   curString.append(oriString[curLevel]); //一旦选了，就一直选，一旦没选，就永远不选
   helper(oriString, curString, ret, curLevel + 1);
   curString.deleteCharAt(curString.length() - 1);
   // no add
   while (curLevel + 1 < oriString.length && oriString[curLevel] == oriString[curLevel + 1]) {
     curLevel++;
   } // 这时候是重复的最后一个元素, 不能放前面，因为你这样就跳到很后面的level了
   helper(oriString, curString, ret, curLevel + 1);
 }
}
```



#### Method 2（只取第一个&& i == index || nums\[i] != nums\[i - 1] && 注意while的位置和while的条件是看在同一层，下一次加的点一不一样）

<mark style="color:blue;">Step 1：分析为什么会发生重复，画图</mark>

* 为什么会重复？同一层分支中，同样的元素，先加前面哪个和先加后面哪个

<mark style="color:blue;">Step 2：说出去重的方法</mark>

* 同一层分支中，同样的元素，我只留第一分支
* 所以不是到了那个点吃吐，而是吃完以后，之后所有的我都不管了
* 为了达到这个效果，我必须得用sort，因为需要把相同的放在一起·



List Version

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null ||| nums.length == 0) {
        return result;
    }
    Arrays.sort(nums);
    List<Integer> current = new ArrayList<>();
    backTracking(result, nums, current, 0);
    return result;
}
// index：当前层我从哪个index往后可以开始考虑呢？
private void backTracking(List<List<Integer>> result , int[] nums, List<Integer> current, int index) {
    // 一个个加很多题目没有base case那都是解
    result.add(new ArrayList<>(current));
    for (int i = index; i < nums.length; i++) {
        if (i != index && nums[i] == nums[i - 1]) {
            continue;
        }
        current.add(nums[i]);
        backTracking(result, nums, current, i + 1);
        current.remove(current.size() - 1);
    }
}

```



String Version

```java
/*
Clarification:
 Input: a String set(String)
 Output: a List of String ret(List<String>)
 repeat!!! && no fix length output

High Level:
 combination problem ----- dfs backtracking ---- 每层多加一个元素

Details:
Recursion tree example: "abb"
                                 ""                ---- curString size 0
                   /              |          \
                "a"               "b"        "b"(no choose)   ---- curString size 1
            /   |                 |        
       "ab"   "ab"(no choose)    "bb"                         ---- curString size 2
        /
    "abb"  
 1) for this recursion tree, each level we decide to add a new element into our curString.
 2) for example, level 1, we can choose 'a', 'b', or 'b'. for level 2, we can only choose the char
    after its previous char, so for level 1 if we choose 'a', for level 2, we can only choose 'b' 'b'
 3) we do this recursively, until we pick all the possible

Key parameter:
 1) curPoss: it carries the beginning position of the element pass from parent's node

Add result & Base case
 1) when all possible check
 2) add result each time

TC: O(2^n), SC: O(n)
*/
public class Solution {
 public List<String> subSets(String set) {
   // Write your solution here.
   List<String> ret = new ArrayList<>();
   if (set == null) {
     return ret;
   }
   StringBuilder curString = new StringBuilder();
   char[] oriString = set.toCharArray();
   Arrays.sort(oriString);
   helper(oriString, curString, ret, 0);
   return ret;
 }
 private void helper(char[] oriString, StringBuilder curString, List<String> ret, int curPoss) {
   ret.add(curString.toString());
   for (int i = curPoss; i < oriString.length; i++) {
     if (i == curPoss || oriString[i] != oriString[i - 1]) {
       curString.append(oriString[i]);
       helper(oriString, curString, ret, i + 1);// 注意这里！！！！！
       curString.deleteCharAt(curString.length() - 1);
     }
   }
 }
}
```







#### Method 3& 4（不sorted & 用set chasing result）

这里的set：是你路过的，但是你不能使用element

* 如果是方法1，你路过的，只有parent和children，还有上下
* 如果是方法2，你路过的，不止是parent，还有你隔壁的children，所以是左右，还有上下
* 这个hashSet是你之前走过路，所以info是到这一层，以及这一层你前面走过的element

```java
public class AllSubSets4 {
   public List<String> subSets(String set) {
       List<String> ret  = new ArrayList<>();
       if (set == null) return ret;
       StringBuilder curString = new StringBuilder();
       Set<Character> curSetForbitedUse = new HashSet<>();
       // dfsHelper1(curString, set, 0, ret, curSetForbitedUse);
       dfsHelper2(curString, set, 0, ret, curSetForbitedUse);
       return ret;
   }

   /// 三个branches
   // cur可以用
       // cur的传到下一层可以用，所以不加入set
       // cur的传到下一层不可以用，所以加入set
   // cur本身就不能用

   private void dfsHelper1(StringBuilder curString, String originalString, int curLevel, List<String> list, Set<Character> curSetForbitedUse) {

       if (curLevel == originalString.length()) {
           list.add(curString.toString());
           return;
       }
       char cur = originalString.charAt(curLevel);
       if (!curSetForbitedUse.contains(cur)) {
           curString.append(cur);
           dfsHelper1(curString, originalString, curLevel + 1, list, curSetForbitedUse);
           curString.deleteCharAt(curString.length() - 1);  
           curSetForbitedUse.add(cur);
           dfsHelper1(curString, originalString, curLevel + 1, list, curSetForbitedUse);
           curSetForbitedUse.remove(cur);
       }
       else {
           dfsHelper1(curString, originalString, curLevel + 1, list, curSetForbitedUse);
       }   
   }

   /// 三个branches
   // cur可以用
       // cur的传到下一层可以用，所以不加入set
       // cur的传到下一层不可以用，所以加入set
   // cur本身就不能用
   private void dfsHelper2(StringBuilder curString, String originalString, int curPossPosition, List<String> list, Set<Character> curSetForbitedUse) {

       // if (curLevel == originalString.length()) {
       //     list.add(curString.toString());
       //     // System.out.println(list);
       //     return;
       // }
       list.add(curString.toString());
       System.out.println(list); 
       List<Character> temp = new ArrayList<>();
       for (int i = curPossPosition; i < originalString.length(); i++)  {
           char cur = originalString.charAt(i);
           //curSetForbitedUse
           // case 1:
           if (!curSetForbitedUse.contains(cur)) {
               curString.append(cur);
               dfsHelper2(curString, originalString, i + 1, list, curSetForbitedUse);
               curString.deleteCharAt(curString.length() - 1);  
               curSetForbitedUse.add(cur); // 这是给这一层,你的下一个是用for loop来
               temp.add(cur); // 这是给这一层的
           }
          
       }
       for (char _temp : temp) {
           curSetForbitedUse.remove(_temp);
       }
   }

   public static void main(String[] args){
       AllSubSets4 test = new AllSubSets4();
       List<String> ret = test.subSets("abba");
       System.out.println(ret);
   }
}
```

