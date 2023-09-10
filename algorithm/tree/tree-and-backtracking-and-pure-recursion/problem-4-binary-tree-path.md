# Problem 4 Binary Tree Path

```java
// Some code

public List<String> binaryTreePaths(TreeNode root) {
    List<String> result = new ArrayList<>();
    
    
    // base case
    if (root == null) {
        return result;
    }
    if (root.left == null. || root.right == null) {
        result.add(root.val + '');
        return result;
    }
    // subproblem
    List<String> leftSubproblemResult = binaryTreePaths(root.left);
    List<String> rightSubproblemResult = binaryTreePaths(root.right);    
    // recursion rule
    for (String path)
}
```





backtracking和pure recursion区别？

backtracking？

* 什么是一个解？一条root to leaf path就是一个解
* high level是什么？
  * 每一层在做什么？
    * 每一层加一个点
  * 分支在做什么？
    * 要么去左，要么去右
  * 一共多少层？
    * n层
* recursion tree





Question：为什么要吃吐守恒？

* 是在子问题吃吐



```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        List<TreeNode> current = new ArrayList<>();
        backTracking(result, current, root);
        return result;
    }
    private void backTracking(List<String> result, List<TreeNode> current, TreeNode root) {
        // 每一层加一个点
        current.add(root);
        // 什么时候手机solution： leaf节点收集solution
        if (root.left == null && root.right == null) {
            // 注意这一行
            current.remove(current.size() - 1);
            result.add(addArrow(current));
            return;
        }
        // branch 要么去左，要么去右
        if (root.left != null) {
            backTracking(result, current, root.left);
        }
       if (root.right != null) {
            backTracking(result, current, root.right);
        }
        current.remove(current.size() - 1);
        // return;
    }
    private String addArrow(List<TreeNode> current) {
        StringBuilder sb = new StringBuilder();
        for (TreeNode temp: current) {
            sb.append(temp.val).append('->');
        }
        return sb.subString(0, sb.length() - 2);
    }

}
```
