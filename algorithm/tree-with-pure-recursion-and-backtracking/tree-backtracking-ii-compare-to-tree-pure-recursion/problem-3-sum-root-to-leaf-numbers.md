# Problem 3 Sum Root to Leaf Numbers

method 1: backtracking

````java
// Some code
```java
/*
Clarification & Assumption
    - Input: it is binary tree, input is a tree node, all with value 0-9
    - Output: all the root to leaf node, and sum them up
High Level
    - backtracking from top to down
Middle Level
    - base case/ return result
        - cur == null, return
        - cur.left == null && cur.right == null, 
            - prevResult * 10 + cur.val
            - update globalResult(since we find a valid solution)
    - cur stage/ induction rule
        - curResult = prevResult * 10 + cur.val
    - subproblem
        - cur.left, cur.right

Recursion Tree
    - branch, left right
    - level: add one node in current level
TC & SC : O(n), O(height)
*/
class Solution {
    public int sumNumbers(TreeNode root) {
        int[] globalResult = new int[]{0};
        if (root == null) {
            return globalResult[0];
        }
        int sumBeforeCur = 0;
        backTracking(root, sumBeforeCur, globalResult);
        return globalResult[0];
    }
    private void backTracking(TreeNode cur, int sumBeforeCur, int[] globalResult) {
        if (cur == null) {
            return;
        }
        if (cur.left == null && cur.right == null) {
            sumBeforeCur =  sumBeforeCur * 10 + cur.val;
            globalResult[0] += sumBeforeCur;
            sumBeforeCur /= 10;
            return;
        }
        sumBeforeCur = sumBeforeCur * 10 + cur.val;
        if (cur.left != null) {
            backTracking(cur.left, sumBeforeCur, globalResult);
        }
        if (cur.right != null) {
            backTracking(cur.right, sumBeforeCur, globalResult);
        }
        sumBeforeCur /= 10;
    }
}
```
````
