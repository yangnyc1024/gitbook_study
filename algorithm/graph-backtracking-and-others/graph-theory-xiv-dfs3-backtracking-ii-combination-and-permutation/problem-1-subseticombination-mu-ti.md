# Problem 1 Subset I (combination)母题

#### Method 1: 加或者不加（只对combination问题有效） ==》 要么要么

High Level：题目让我们求出all subsets

* step1:什么是一个解？一个subset是一个解
* step2:如何构造一个解？
  * 每一层是什么？考虑一个元素
  * 分支是什么？要么加，要么不加
  * 在哪里收集解？一共有多少层？有多少元素就有多少层
* index：当前层我正要考虑的元素
* index = length -1这个状态，正要考虑最后一个元素
* index = length，这个状态才是考虑完所有元素的状态

one version(List version)

```java
// Some code
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null || nums.length == 0) {
        return result;
    }
    List<Integer> current = new ArrayList<>();
    backTracking(result, nums, current, 0);
    return result;
}
// index我们当前层考虑的元素
private void backTracking(List<List<Integer>> result, int[] nums, List<Integer> current, int index) {
    if (index == nums.length) {
        result.add(new ArrayList<>(current));
        return;
    }
    // add
    current.add(nums[index]);
    backTracking(result, nums, current, index + 1);
    current.remove(current.size() - 1);
    backTracking(result, nums, current, index + 1);
}
```

another version (String version)

```java
/*
Clarification:
 Input: a String set(String)
 Output: a List of String ret(List<String>)
 no repeat && no fixed length output


High Level:
 combination problem ----- dfs backtracking ---- each step choose or not choose


Middle Level:
 Recursion tree example: "abc"

                        ""
                 /              \
               ""                "a"       ----- level 1            
           /         \        /          \
         ""         "b"    "a"         "ab"    ---- level 2          
    /     \        /     \ 
""         "c"   "b"   "bc". .... ----- level 3

 1) for each level, we decide if we choose a new element, for example level one , we decide to choose 'a' or not.
 2) We do this recursively. It means based on level 1 result, for level 2, we decide choose or not 'b',
     which is the second element in the oriString.
 3) when we iterate all the possible element we can choose, it means we reach oriString.length(), we output our result;


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
   helper(set, curString, ret, 0);
   return ret;
 }

 private void helper(String origString, StringBuilder curString, List<String> ret, int curLevel) {
   if (curLevel == origString.length()) {
     ret.add(curString.toString());
     return;
   }
   curString.append(origString.charAt(curLevel));
   helper(origString, curString, ret, curLevel + 1);
   curString.deleteCharAt(curString.length() - 1);
   helper(origString, curString, ret, curLevel + 1);
 }
```

Question to deep dive: 能不能先写这个不加，这样是不是就可以不用吐了

* 万万不可
* 吃吐必须守恒，就算没有显示的吐，也一定通过某种方式达到吐的效果，直接吃掉吐又没有做任何补充，肯定不对！
* 原因是什么？在一个path上visited过的不能再visited？





#### Method 2:一个一个加（**每一层是元素有几个，像permutation**）

Step 1: 什么是一个解？一个subset就是一个解（题目让你做什么）

Step 2:如何构造一个subset

* 每一层：考虑这一层所有可以加的元素
* 分支：这一层把谁加进来
* 在哪里收集解：哪里都是解

相当于人为的自己加一个order：为了保证不发生由于顺序带来的重复

TC \&SC: O(2^n), O(n)





one version(List version)

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null || nums.length == 0) {
        return result;
    }
    List<Integer> current = new ArrayList<>();
    backTracking(result, nums, current, 0);
    return result;
}

// index:当前层我从哪个index往后可以开始考虑加呢？
private void backTracking(List<List<Integer>> result, int[] nums, List<Integer> current, int index) {
    // 一个个加很多题目没有base case那都是解
    result.add(new ArrayList<>(current));
    for (int i = index; i < nums.length; i++) {
        current.add(nums[i]);
        backTracking(result, nums, current, i + 1);
        current.remove(current.size() - 1);
    }
}
```

another version (String version)

```java
/*
Clarification:
Input: a String set(String)
Output: a List of String ret(List<String>)
no repeat && no fixed length output


High Level:
combination problem ----- dfs backtracking ---- each step choose or not choose


Details:
Recursion tree example: "abc"
                      ""                                    ---- curString size 0
                   /           |             \
                 "a"        "b"           "c"  ---- curString size 1
             /  |    \      /     \     
        "ab"    "ac"  "bc"       ---- curString size 2 :
         /
     "abc"   
 1) for this recursion tree, each level we decide to add a new element into our curString.
 2) for example, level 1, we can choose 'a', 'b', or 'c'. for level 2, we can only choose the char
     after its previous char, so for level 1 if we choose 'a', for level 2, we can only choose 'b' 'c'
 3) we do this recursively, until we pick all the possible,

Key parameter:
 1) curPoss: it carries the beginning position of the element pass from parent's node

Add result & Base case
1) when all possible check
2) add result each time

TC : O(2^n), SC: O(n)
C(n,1) + C(n,2) +...+ C(n,n) ~= O(2^n)
*/


public class Solution {
 public List<String> subSets(String set) {
   // Write your solution here.
   List<String> ret = new ArrayList<>();
   if (set == null) return ret;
   StringBuilder curString = new StringBuilder();
   helper(set, curString, ret, 0);
   return ret;
 }
 private void helper(String oriString, StringBuilder curString, List<String> ret, int curPoss) {
   // base case && return result
   ret.add(curString.toString());
   // subproblem & induction
   for (int i = curPoss; i < oriString.length(); i++) {
     curString.append(oriString.charAt(i));
     helper(oriString, curString, ret, i + 1);
     curString.deleteCharAt(curString.length() - 1);
   }

 }
}
```
