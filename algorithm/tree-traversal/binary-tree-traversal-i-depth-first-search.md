# Binary Tree Traversal I Depth First Search

## Tree Traversal

<figure><img src="../.gitbook/assets/Screenshot 2023-09-21 at 10.10.53 PM.png" alt=""><figcaption></figcaption></figure>



## Part I: DFS Recursion实现

* 注意这颗特别的树

<figure><img src="../.gitbook/assets/Screenshot 2023-09-21 at 10.15.12 PM.png" alt=""><figcaption></figcaption></figure>



#### DFS遍历的本质（核心要点）

注意走三次，pre，in，post，第几次回就是对应的，i.e.



#### DFS遍历的本质（核心要点）

* 一笔画走完每一个分支，每个其实会经过三次，
  * 第一次经过，就是DFS preOrder
    * 也是从你的parent call的时候，从上到下的过程
  * 第二次经过，就是DFS inOrder
    * 从你的左子树回来的时候经过你的过程，从下到上的过程
  * 第三次经过，就是DFS postOrder
    * 从你的右子树回来的时候最后一次经过你的时候（马上下一站该会parent）：从下到上的过程





## Part II: DFS Iteration 实现



#### 版本1(可以给preOrder & inOrder)

```java
// Some code

public void generalDFS(Tree){
    TreeNode cur = root;
    Deque<TreeNode> stack = new ArrayDeque<>();
    while(cur != null || !stack.isEmpty()) {
        if (cur != null) {
            stack.push(cur);
            cur = cur.left;
        }else {
            cur = stack.pop();
            cur = cur.right;
        }
    }
}
```

* 经过这个概念，第几次经过，第一次，第二次都好，但是第三次不行
* 我们总是在第二次经过的时候就给他pop出来，然后我们就没有机会第三次cur赋予为这个node

#### 版本2(错误)

```java
// Some code
public void generalDFS(Tree){
    TreeNode cur = root;
    Deque<TreeNode> stack = new ArrayDeque<>();
    while(cur != null || !stack.isEmpty()) {
        if (cur != null) {
            stack.push(cur);
            cur = cur.left;
        }else {
            cur = stack.peek();
            cur = cur.right;
        }
    }
}
```

* 问题更大，不是不好表达，根本就是错误，这个while循环可能进不去么？单反是有一个点进去了，全程没有pop
* 第一次，第二次都没有问题，第三次本来就应该是pop出来，第三次也peek了，第四次，第五次。。。。
* 根本问题在于：所以第二次和第三次经过的本质区别是啥？
  * 第二次和第三次经过这个点他们的本质区别在哪？方向不同？第二次经过他是从左子树回来，而第三次经过它是从右子树回来
  * 所以可以用prevNode，知道上一次访问的（visit）的node如果是左子树的根节点，那我一定是第二次经过你啊我是从你左边回来的，如果我上一次访问的（visit）的node如果是右子树的根节点，那我一定是第三次是经过你了因为我是从你的右边回来的



#### 版本3 加个lastVisited(可以给postOrder)

* 如果我只是想写post order，其实我不需要知道我是第几次经过这个点，而我更需要知道的是我从哪个点访问完以后才来经过当前点的，看从左还是从右回来就可以了

```java
// Some code


public void generalDFS(TreeNode root) {
    TreeNode cur = root;
    Deque<MyTreeNode> stack = new ArrayDeuque<>();
    List<Integer> result = new ArrayList<>();
    TreeNode lastVisited = null; //上一次postOrder访问的点是谁呢？
    while (cur != null || !stack.isEmpty()) {
        if (cur != null) {
            cur.count++;
            
            stack.push(cur);
            cur = cur.left;
        }
        else {
            TreeNode peekNode = stack.peek();
            if (peekNode.right != null) && lastVisited != peekNode.right) {
                //有右边，而且你不是从右边回来，而且你还在else分支里，第二次经过被
                cur = peekNode.right;
            }else {
                // 要么你没右子树，要么你虽然右子树但是你刚从那边回来，访问完右子树
                result.add(peekNode.val);
                lastVisited = stack.pop();
            }     
        }
    }
    return result;
}
```

#### 版本4 自己数啥时候经过

count：就是第几次经过

```java
// Some code
class MyTreeNode {
    TreeNode node;
    int count;
    public MyTreeNode(TreeNode root) {
        this.node = root;
    }
}

public void generalDFS(MyTreeNode root) {
    MyTreeNode cur = new MyTreeNode(root);
    Deque<MyTreeNode> stack = new ArrayDeuque<>();
    List<Integer> result = new ArrayList<>();
    while (cur != null || !stack.isEmpty()) {
        if (cur != null) {
            cur.count++;
            //result.add(cur);
            stack.push(cur);
            cur = new MyTreeNode(cur.node.left);
        }
        else {
            MyTreeNode peekNode = stack.peek();
            peekNode.count++;
            if (peekNode.count == 3) {
                // this is the last bus
                //result.add(peekNode.node.val);
                stack.pop();
            }
            if (peekNode.count == 2) {
                //result.add(peekNode.node.val);
                if (peekNode.node.right != null) {
                    cur = new MyTreeNode(peekNode.node.right);
                }
            }
        }
    }
}
```

