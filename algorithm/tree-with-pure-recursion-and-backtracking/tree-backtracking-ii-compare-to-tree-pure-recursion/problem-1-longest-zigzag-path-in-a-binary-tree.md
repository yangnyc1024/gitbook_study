# Problem 1 Longest ZigZag Path in a Binary Tree

### Method 1 Backtracking

````java
// Some code

```java

 /*
Assumption & Clarification
    - input: regular binary tree
    - output: longest path from any node to any node, the maximum path length
High Level
    - backtracking from top to buttom to search all path from node to node
Middle Level
    - base case,
        -  null return
    - return result
        - each time
    - each Level
        - valid node from current Level
    - branches
        - left, right (if they exists)
Recursion TreeNode.  
                                     cur
                    /               \               \                        \
               (!isleft,cur.left) (isleft, cur.left)   (!isleft, cur.right)   (!isleft, cur.right)   
                /.    \.     /.    \.  
      
TC & SC O(n), O(1)
 */
class Solution {
    public int longestZigZag(TreeNode root) {
        int[] globalMax = new int[]{0};
        if (root == null) {
            return globalMax[0];
        }
        int curPossLength = 0;
        backTracking(root, curPossLength, true, globalMax);
        backTracking(root, curPossLength, false, globalMax);
        return globalMax[0];
    }
    private void backTracking(TreeNode cur, int curPossLength, boolean isPrevLeft, int[] globalMax) {
        // base case 
        if (cur == null) {
            return;
        }
        // return result
        globalMax[0] = Math.max(globalMax[0], curPossLength);
        curPossLength++;

        // current , induction rule?
        // subproblem
        if (isPrevLeft) { // previous is left
            backTracking(cur.left, 1, true, globalMax); // 这里是1
            backTracking(cur.right, curPossLength, false, globalMax);
        } 
        else { // previous is right
            backTracking(cur.left, curPossLength, true, globalMax);
            backTracking(cur.right, 1, false, globalMax);
        }
        curPossLength--;
    }
}
```java
````

### Method 2 Pure Recursion

````java
// Some code

```java
 /*
Assumption & Clarification
    - input: regular binary tree
    - output: longest path from any node to any node, the maximum path length
High Level
    - pure recursion from buttom to up
Middle Level
    - function:
        getting info for cur nofr as root, cur root as left, cur root as right, globalMax
    - base case
        cur == null
    - subproblem
        leftResult, rightResult
    - recursive rule
        curRight = max (1 + rightResult.left, 1);
        curLeft = max (1 + leftResult.right, 1);
        globalMax =  max (max(curRight, curLeft), max(leftMax, rightMax));
 */
class Solution {
    public int longestZigZag(TreeNode root) {
        if (root == null) {
            return 0;
        }
        ReturnType result = recursion(root);
        return result.maxLength - 1;

    }
    private ReturnType recursion(TreeNode cur) {
        if (cur == null) {
            return new ReturnType(0, 0, 0);
        }
        ReturnType leftResult = recursion(cur.left);
        ReturnType rightResult = recursion(cur.right);
        int curLeft = Math.max(1 + leftResult.curRightMax, 1);
        int curRight = Math.max(1 + rightResult.curLeftMax, 1);
        int max = Math.max(Math.max(leftResult.maxLength, rightResult.maxLength), Math.max(curLeft, curRight));
        return new ReturnType(max, curLeft, curRight);
    }
    class ReturnType {
        int maxLength;
        int curLeftMax;
        int curRightMax;
        public ReturnType(int maxLength, int curLeftMax, int curRightMax) {
            this.maxLength = maxLength;
            this.curLeftMax = curLeftMax;
            this.curRightMax = curRightMax;
        }
    }
}
```
````
