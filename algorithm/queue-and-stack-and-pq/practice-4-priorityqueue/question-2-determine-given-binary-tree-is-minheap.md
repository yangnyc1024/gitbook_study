# Question 2 Determine given Binary Tree is minHeap

```java
public boolean isMinHeap(TreeNode root) {
    if(root == null) {
        return true;
    }
    return treeIsComplete(root) && isMinAtEveryRoot(root);
}

private boolean isMinAtEveryRoot(TreeNode root) {
    if (root == null) {
        return true;
    }
    if (root.left == null && root.right == null) {
        return false;
    }
    if (root.left != null && root.left.key < root.key) {
        return false;
    }
    if (root.right != null && root.right.key < root.key) {
        return false;
    }
    return isMinAtEveryRoot(root.left) && isMinAtEveryRoot(root.right);
}


private boolean treeIsComplete(TreeNode root) {
    boolean metNullBefore = false;
    Queue<TreeNode> queue = new ArrayDequ<>();
    // ArrayQueue 在做Tree和Graph问题的时候,小心不能装null；
    queue.offer(root);
    while (!queue.isEmpty()) {
        TreeNode cur = queue.poll();
        if (cur.left == null) {
            if (metNullBefore == false) {
                metNullBefore = true;
            } else {
                if (metNullBefore == true) {
                    return false;
                }
                queue.offer(cur.left);
            }
        } 
        
        if (cur.right == null) {
            if (metNullBefore == false) {
                metNullBefore = true;
            } else {
                if (metNullBefore == true) {
                    return false;
                }
                queue.offer(cur.right);
            }
        }  
        return true;  
    }
```
