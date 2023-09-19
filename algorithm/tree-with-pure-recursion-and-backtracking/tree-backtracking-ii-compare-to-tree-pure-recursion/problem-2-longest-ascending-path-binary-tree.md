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
