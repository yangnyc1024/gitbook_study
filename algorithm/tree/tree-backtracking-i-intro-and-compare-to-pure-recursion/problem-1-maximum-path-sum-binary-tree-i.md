# Problem 1 Maximum Path Sum Binary Tree I

* be careful if you have left or right node
* 注意，这个因为是leaf 到leaf，所以在该点的时候，只有它左边有，右边有，两边都有的时候才能更新

```java
 /*
 Clarification & Assumption:
  - Input: a normal binary tree, with integer value, 
  - Output: the maximum path, from leaf to leaf
  - example: 
              1
            /   \
          3      5
        /   \
      4     -1 
      4 + 3  + 5 + 1

              -1
            /   \
          3      5
        /   \
      4     -1 
      for -1 , we get 4 + 3, we also get 5,  4 +3 - 1 + 5
      for 3, we get 4 + -1 + 3
  High Level
    - pure recursion from bottom to up
  Middle Level
    - function meaning: given a node, return the maximum path from any leaf to current node as the root
    - base case
      - cur == null
      - cur.left == null || cur.right == null
    - subproblem
      - cur.left, cur.right
    - recursion rule
      -  leftMaxPath , righgMaxPath
      - 这里应该是有四种情况！！！！除去base case 还有三种
      -  !!! 不是每次都更新，唯有两边都有才更新！！！！
        - update gloMax = max(globalMax, leftMaxPath + rightMaxPath + cur.Val)
        - return Math.max(leftMaxPath, rightMaxPath) + cur.val
      - 如果有一边没有，
        - 不更新
        - return有的那一边
 */
public class Solution {
  public int maxPathSum(TreeNode root) {
    // Write your solution here
    // sanity check
    if (root == null) {
      return 0;
    }
    //
    int[] globalMax = new int[]{Integer.MIN_VALUE};
    helper(root, globalMax);
    return globalMax[0];
  }
  private int helper(TreeNode cur, int[] globalMax) {
    if (cur == null) {
      return 0;
    }
    if (cur.left == null && cur.right == null) {
      return cur.key;
    }
    int leftMaxPath = helper(cur.left, globalMax);
    int rightMaxPath = helper(cur.right, globalMax);
    if (cur.left != null && cur.right != null) {
      globalMax[0] = Math.max(globalMax[0], leftMaxPath + rightMaxPath + cur.key);
      return Math.max(leftMaxPath, rightMaxPath) + cur.key;
    }
    return cur.left == null ? rightMaxPath + cur.key : leftMaxPath + cur.key;
  }
}
```
