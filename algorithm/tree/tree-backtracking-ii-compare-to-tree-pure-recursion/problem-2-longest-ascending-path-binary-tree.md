# Problem 2: Longest Ascending Path Binary Tree



Method 1: backtracking version 1

```java
// Some code
/**
 * public class TreeNode {
 *   public int key;
 *   public TreeNode left;
 *   public TreeNode right;
 *   public TreeNode(int key) {
 *     this.key = key;
 *   }
 * }
 */

/*
Clarification & Assumption
  - input: a binary tree node
  - output: the length of maximum path from any node to any leaf node
High Level
  - backtracking from top to bottom

Example: 
              5
            /.  \
          3.     2. 
      /    \.    /.  \ 
      1.   0          11
      5,
      for 3, 
                          
Middle Level
  - function, 
    - carrying the info with currentNode like a end node, to update the maximum path from definition
  - Base case, leaf node 
    - add leaf value to all paths in curResult 
    - add curResult' maximum path to result
  - curr step
    - add current node, 
  - subproblem
    - cur.left, cur.right
Recursion Tree
  - level: inherit or not inherit the path ending to curResult to left or right
  - branch: 
      left: add curMax or not curMax to left 
      right: add curMax or not curMax to right 
TC & SC: O(n), O(height)
*/
/*
maxPathEndCur: have already add cur
globalMathPathEndBeforeCur: have not add cur

*/
public class Solution {
  public int longest(TreeNode root) {
    // Write your solution here
    int[] globalMathPathEndBeforeCur = new int[]{0};
    if (root == null){
      return globalMathPathEndBeforeCur[0];
    }
    int maxPathEndCur = 1;
    backtracking(root, maxPathEndCur,globalMathPathEndBeforeCur);
    return globalMathPathEndBeforeCur[0];
  }
  private void backtracking(TreeNode cur, int maxPathEndCur, int[] globalMathPathEndBeforeCur) {
    // base case
    // return result
    if (cur == null) {
      // do not need to update since it is for before
      // globalMathPathEndBeforeCur[0] = Math.max(globalMathPathEndBeforeCur[0], maxPathEndCur);
      return;
    }
    globalMathPathEndBeforeCur[0] = Math.max(globalMathPathEndBeforeCur[0], maxPathEndCur);
    // cur
    if (cur.left != null) {
      if (cur.left.key > cur.key) {
        maxPathEndCur++;
        backtracking(cur.left, maxPathEndCur, globalMathPathEndBeforeCur);
        maxPathEndCur--;
      }
      backtracking(cur.left, 1, globalMathPathEndBeforeCur);
    }
    if (cur.right != null) {
      if (cur.right.key > cur.key) {
        maxPathEndCur++;
        backtracking(cur.right, maxPathEndCur, globalMathPathEndBeforeCur);
        maxPathEndCur--;
      }
      backtracking(cur.right, 1, globalMathPathEndBeforeCur);
    }

    // next problem
  }
}

```

Method 2: backtracking version 2!!!!

```java
// Some code
public class Solution {
  public int longest(TreeNode root) {
    // Write your solution here
    int[] globalMathPathEndBeforeCur = new int[]{0};
    if (root == null){
      return globalMathPathEndBeforeCur[0];
    }
    backtracking(root, 0 , globalMathPathEndBeforeCur);
    return globalMathPathEndBeforeCur[0];
  }
  private void backtracking(TreeNode cur, int maxPathEndBeforeCur, int[] globalMathPathEndBeforeCur) {
    // base case
    // return result
    if (cur.left == null && cur.right == null) {
      maxPathEndBeforeCur++;
      globalMathPathEndBeforeCur[0] = Math.max(globalMathPathEndBeforeCur[0], maxPathEndBeforeCur);
      maxPathEndBeforeCur--;
      return;
    }
    // add cur, what happen?
    maxPathEndBeforeCur++;
    globalMathPathEndBeforeCur[0] = Math.max(globalMathPathEndBeforeCur[0], maxPathEndBeforeCur);
    // cur
    if (cur.left != null) {
      if (cur.left.key > cur.key) {
        backtracking(cur.left, maxPathEndBeforeCur, globalMathPathEndBeforeCur);
      }
      backtracking(cur.left, 0, globalMathPathEndBeforeCur);
    }
    if (cur.right != null) {
      if (cur.right.key > cur.key) {
        backtracking(cur.right, maxPathEndBeforeCur, globalMathPathEndBeforeCur);
      }
      backtracking(cur.right, 0, globalMathPathEndBeforeCur);
    }
    maxPathEndBeforeCur++;
    // next problem
  }
}

```

Method 2: Pure Recursion

```java
// Some code
/*
Clarification & Assumption
  - input: a binary tree node
  - output: the length of maximum path from any node to any leaf node
High Level
  - pure recursion from bottom to up

Example: 
              5
            /.  \
          3.     2. 
      /    \.    /.  \ 
      1.   0          11
      5,
      for 3, 
                          
Middle Level
  - function, 
    - given the cur root, return the length of maximum path from any leaf to cur root
    - with globalMax
  - Base case
    - cur.left == null && cur.right == null
    - return 1;
  - subproblem
    - leftResult, rightResult
  - recursive rule
    - cur.left != null && cur.right == null
    - cur.left == null && cur.right != null
    - cur.left != null && cur.right != null
    if (cur.left.val > cur.val) curLeftInher += leftResult; update globalMax
    if (cur.right.val > cur.val) curRightInher += rightResult; update globalMax
  - return?
     return max(curleftInher, curRightInher) + 1;
      
TC & SC: O(n), O(height)
*/
/*
maxPathEndCur: have already add cur
globalMathPathEndBeforeCur: have not add cur

*/
public class Solution {
  public int longest(TreeNode root) {
    // Write your solution here
    int[] globalMax = new int[]{0};
    if (root == null) {
      return globalMax[0];
    }
    helper(root, globalMax);
    return globalMax[0];
  }
  private int helper(TreeNode cur, int[] globalMax) {
    if (cur == null) {
      return 0;
    }
    if (cur.left == null && cur.right == null) {
      globalMax[0] = Math.max(globalMax[0], 1);
      return 1;
    }
    int leftBeginMaxPath = helper(cur.left, globalMax);
    int rightBeginMaxPath = helper(cur.right, globalMax);
    int curResult = 1;
    if (cur.left != null && cur.left.key > cur.key) {
      curResult = Math.max(curResult, leftBeginMaxPath + 1);
    }
    if (cur.right != null && cur.right.key > cur.key) {
      curResult = Math.max(curResult, rightBeginMaxPath + 1);
    }
    globalMax[0] = Math.max(globalMax[0], curResult);
    return curResult;
  }
}
```
