---
description: Question 7
---

# Question 7 Binary Tree Upside Down

Middle Level





Step 1 function\
\- 给你upside down好以root为跟的subtree并且返回upside down以后的新的root节点

Step 2: base case\
\- root == null\
\- root.left == null, return root

Step 3: subproblem\
\- root.right

Step 4: Recursive Rule\
\- original problem？\
\- subproblem？\
\- subproblem solution？

？？？？







## Method 2&#x20;

<mark style="color:purple;">LeftSubTree Upside-Down = LeftSubtree view as a LinkedList Reversion</mark>\


```java
public TreeNode upsideDownBinaryTree(TreeNode root) {
    if (root == null || root.left == null) {
        return root;
    }
    TreeNode prev = null;
    TreeNode cur == root;
    TreeNode right = null;
    while (cur != null) {
        TreeNode next = cur.left;
        TreeNode newright = cur.right;
        cur.right = prev;
        cur.left = right;
        right = newRight;
        
        prev = cur;
        cur = next;
    }
    return prev
}
```

