---
description: recursion
---

# Problem 2 Maximum Path Sum Binary Tree II 标准recursion模版

```java
/*
Clarification & Assumption
  - Input: Root , regular binary tree
  - Output: the maximum path from any node to any node
  - Example:
              1
           /     \
          2       3
        /   \      
      4      -5
      4, -5
      2, 2 + 4, 2 -5 , 2 +4 -5
      1 with 2 as root(2, 2 +4 , 2 - 5),  1 with 3, 1 with 2, 3, 1 itself


High Level
  - pure recursion to find maximum path from bottom to up

Middle Level
  - function meaning: given a root, we pass the maximum path(any node including itself) ends with cur node as root
  - base case
    - cur == null
    - cur.left == null && cur.right == null
  subproblem
    - leftPath, rightPath
  recursive rule
    - we get leftPath and rightPath
        - if we update leftPath = max(leftPath, 0), rightPath = max(rightPAth, 0);
    - cur.left && cur.right 
      - current possible result:
          - glaobalMax = max (globalMax, leftPath + cur, rightPath + cur, cur, leftPath + rightPath + cur)
      - return?
          - max(leftPath + cur, rightPath + cur, cur)
    - cur.left == null && cur.right 
      - current possible result:
          - glaobalMax = max (globalMax, rightPath + cur, cur)
      - return?
          - max( rightPath + cur, cur)
    - cur.left && cur.right == null 
      - current possible result:
          - glaobalMax = max (globalMax,leftPath + cur, cur)
      - return?
          - max(leftPath + cur,  cur)
TC & SC O(n), O(1)

    alternative: we can do combine
    - update leftPath = max(leftPath, 0), rightPath = max(rightPAth, 0);
    - globalMax = math( cur.key, cur.key + rightResult + leftResult);
    - return root.key + Math.max(leftSum, rightSum)
*/
public class Solution {
  public int maxPathSum(TreeNode root) {
    // Write your solution here
    if (root == null) {
      return 0;
    }
    int[] result = new int[]{Integer.MIN_VALUE};
    recursion(root, result);
    return result[0];
  }
  private int recursion(TreeNode cur, int[] result) {
    if (cur == null) {
      return 0;
    }
    if (cur.left == null && cur.right == null) {
      result[0] = Math.max(cur.key, result[0]);
      return cur.key;
    }
    int leftPath = recursion(cur.left, result);
    int rightPath = recursion(cur.right, result);
    if (cur.left != null && cur.right == null) {
      result[0] = Math.max(result[0], leftPath + cur.key);
      result[0] = Math.max(result[0], cur.key);
      return Math.max(leftPath + cur.key, cur.key);
    }
    if (cur.left == null && cur.right != null) {
      result[0] = Math.max(result[0], rightPath + cur.key);
      result[0] = Math.max(result[0], cur.key);
      return Math.max(rightPath + cur.key, cur.key);
    }
    result[0] = Math.max(result[0], leftPath + cur.key);
    result[0] = Math.max(result[0], rightPath + cur.key);
    result[0] = Math.max(result[0], cur.key);
    result[0] = Math.max(result[0], leftPath + rightPath + cur.key);
    int curResult = cur.key;
    curResult = Math.max(curResult, leftPath + cur.key);
    curResult = Math.max(curResult, rightPath + cur.key);
    // leftPath = Math.max(leftPath, 0);
    // rightPath = Math.max(rightPath, 0);
    // result[0] = Math.max(result[0], cur.key + leftPath + rightPath);
    // int curResult = cur.key + Math.max(leftPath, rightPath);
    // return curResult;
  }
}

```
