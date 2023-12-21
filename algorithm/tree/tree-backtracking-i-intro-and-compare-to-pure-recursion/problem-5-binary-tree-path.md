# Problem 5 Binary Tree Path





backtracking和pure recursion区别？



Question：为什么要吃吐守恒？

* 是在子问题吃吐



````java
```java
 /*
Clarification & Assumption
    - input: tree
    - output: all root-to-leaf paths in any order, root- to- leaf
    - example:
                    1
                /       \
              2           3
              \
                5
    1) 1-> 2-> 5, 2) 1-> 3
Method 1: pure recusion
High Level: pure rucursion from bottom to up
Middle Level:
    - function meaning: build the path from leaf to cur path(cur is as root)
    - base case
        - cur == null
        - cur.left == null && cur.right == null
    - subproblem
        - leftPath, rightPath, List<String>
    - recursive rule
        - for String path: leftPath & rightPath
            add cur.val into each path in leftPath, and rightPath
TC & SC:
    - ???

Method 2: backtracking
High Level: backtracking from up to bottom
Middle Level:
    - function meaning: build the path from cur(as Root) to leaf one by one
    - base case && add result?
        - each time add?
        - when it is null, 
    - each Level
        -add one node
    - branch?
        - add left or add right(null case can also work)
    - how many level? 
        - height
TC & SC:
    - ???

 */
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        // List<String> result = new ArrayList<>();
        // if (root == null) {
        //     return result;
        // }
        // List<TreeNode> curResult = new ArrayList<>();
        // backTracking(root, curResult, result);

        if (root == null) {
            return null;
        }
        List<String> result = pureRecursion(root);
        return result;
    }
    private List<String> pureRecursion(TreeNode root) {
        List<String> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        if (root.left == null && root.right == null) {
            result.add(root.val + "");
            return result;
        }
        List<String> leftPath = pureRecursion(root.left);
        List<String> rightPath = pureRecursion(root.right);
        for (String cur: leftPath) {
            result.add(root.val + "->" + cur);
        }
        for (String cur: rightPath) {
            result.add(root.val + "->" + cur);
        }
        return result;
    }
    private void backTracking(TreeNode root, List<TreeNode> curResult, List<String> result) {
        // base case  , return result
        if (root.left == null && root.right == null) {
            curResult.add(root);
            result.add(postAddRow(curResult));
            curResult.remove(curResult.size() - 1);
        }
        // current?
        curResult.add(root);
        // subproblem
        if (root.left != null) {
            backTracking(root.left, curResult, result);
        }
        if (root.right != null) {
            backTracking(root.right, curResult, result);
        }
        curResult.remove(curResult.size() - 1);

    }
    private String postAddRow(List<TreeNode> curResult) {
        StringBuilder sb = new StringBuilder();
        for (TreeNode curNode: curResult) {
            sb.append(curNode.val).append("->");
        }
        return sb.substring(0, sb.length() - 2);
    }
}
```
````
