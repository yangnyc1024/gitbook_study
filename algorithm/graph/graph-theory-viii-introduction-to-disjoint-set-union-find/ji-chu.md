# 基础

#### What is a Union-Finding?

* It is a data structure
* A data structure

#### When?

* 解决图问题
* use case：图是在<mark style="color:purple;">动态变化</mark>

**Why?**

* 代码极其短
* hit use case 时间复杂度

#### 关注点

* 两个集合是不是联通
* 集合==》联通力量
* 性质：每一个集合都有一个代表

#### 思考方式

* 集合代表着帮派
* 集合的代表元素代表帮派老大



#### API

* UnionFind() constructor  构造函数O(n), n as number of node
* union(int a, int b):把a加入b的集合，或者把b加入a的集合
* int find(a):找到a所在集合的代表元素

#### 时间复杂度

* Quick Union -- union find
  * find: O(n)
  * union: O(n)
* Quick Find -- union find
  * find: O(1)
  * union: O(n)
* Weighted/Ranked/OtherRanked Union Find(Tree Array Based)
  * find: O(log n)
  * union O(log n)
* Weight Union Find with Path Compression
  * find: O\*(1)
  * union: O\*(1)
  * where \*: O(loglog(n)) > O(1)

#### How

* Union - Find用数组实现的数据结构
* 假设长度是n -> int\[] laoda
* laoda\[i] 代表i的老大是谁
* count：一共有多少个帮派
* int\[] size -> size\[i]  代表i所在的帮派有多少

#### How: Union Find底板（2min！！！）

<pre class="language-java"><code class="lang-java">class UnionFind{
<strong>    int[] laoda; //有几个帮派的老大, 可能是需要laodaMap map&#x3C;你的类型，帮派的老大>
</strong><strong>    int[] size; //几个帮派的大小
</strong><strong>    int count;
</strong><strong>    public UnionFind(int n){
</strong><strong>        this.laoda = new int[n];
</strong><strong>        this.size = new int[n];
</strong><strong>        this.count = n;
</strong><strong>        for (int i =; i&#x3C; n; i++) {
</strong><strong>            laoda[i] = i;
</strong><strong>            size[i] = 1;
</strong><strong>        }
</strong><strong>    }
</strong><strong>    public int find(int a) {
</strong><strong>    
</strong><strong>    }
</strong><strong>    public void union(int a, int b) {
</strong><strong>    
</strong><strong>    }
</strong><strong>    
</strong>

}
</code></pre>

#### UF时空复杂度

* union,find 都是O\*(1)
* constructor: both O(n)

#### 面试里注意点的和基本逻辑

* 对于find(a):找到的是真老大
* union(a, b): a,b 要先检查需不需要union，如果老大都一样，就不需要用union了

#### 第一种Union-Find: Quick Union

union(a, b)--> 把a加入b

* example:&#x20;
  * laoda: {0, 1, 2},&#x20;
  * union(2, 1),
  * laoda = {0,1,1}
  * union(1, 0)
  * laoda: {0, 0, 1}
  * 其实0，1，2，都在一个联通分量里面，但是观察老大是分级别的
* 谁是真老大？
  * 真老大的特点laoda\[zhenlaoda] = zhenlaoda
* quick union:
  * union 一时爽，find的时候要溯源

```java
public int find(int a) { //这个是用来找真正的老大，就是前面提到的溯源
    while (a != laoda[a]) {
        a = laoda[a];
    }
    return a;
}
public void union(int a, int b){//注意这里是把a加入b
    int alaoda = find(a);
    int blaoda = find(b);
    if (alaoda == blaoda) return;
    laoda[a] = b;
    count--;
    size[blaoda] += size[alaoda];
}
```

TC\&SC:&#x20;

* find: O(n)
* union: O(n)



#### 第二种Union Find: Quick Find

Find O(1)

example:&#x20;

* laoda: {0, 1, 2},&#x20;
* union(2, 1),
* laoda = {0,1,1}
* union(1, 0)
* laoda: {0, 0, 1} ==> {0,0,0}
* 操作上来说，如果要把a的老大改成c，不能只改a，把所有以a为老大的小弟们的老大都改成c（相当于老板跳槽，把他所有学生都带去跳槽）

```java
public int find(int a) {
    return laoda[a];
}
public void union(int a, int b) {
    int alaoda = find(a);
    int blaoda = find(b);
    for (int i = 0; i < laoda.length; i++) { // 把a里面所有的都变成b
        if (laoda[i] = a) {
            laoda[i] = b;
        }
    }
    if (alaoda == blaoda) return;
    laoda[a] = b;
    count--;
    size[blaoda] += size[alaoda];
}
```

TC& SC: Find(1), Union(n)



#### 第三种Union- Find, Weight Union Find => Tree

核心思想：

* union(a,b)刚才是a加入b，or b加入a
* <mark style="color:purple;">现在一定是小的那个，加入大的那个大小</mark>: size\[i]
* 是用tree的形式，越靠近tree的顶，越是那个大的
* example
*

    <figure><img src="../../.gitbook/assets/Screenshot 2023-12-30 at 9.33.44 PM.png" alt="" width="375"><figcaption></figcaption></figure>

```java
public int find(int a) {
    while(a != laoda[a]) {
        a = laoda[a];
    }
    return a;
}
public void union(int a, int b) {
    int alaoda = find(a);
    int blaoda = find(b);
    if (alaoda == blaoda) return;
    if (size[alaoda] >= size[blaoda]) {
        laoda[blaoda] = alaoda // 不是laoda[b] = a; 
        size[alaoda] += size[blaoda];
    }
    else{
        laoda[alaoda] = blaoda;
        size[blaoda] += size[alaoda];
    }
}
```

* 这里相当于size是weight

#### 第四种Union-Find：Weighted Union FInd with PathCompression

* Path Compression：路径压缩
* 路径压缩精髓：苟富贵勿相忘(一个人富贵了，所有帮助给你的人全都浮过)
* example
*

    <figure><img src="../../.gitbook/assets/Screenshot 2023-12-30 at 9.46.36 PM.png" alt="" width="375"><figcaption></figcaption></figure>

```java
//细节版本
public int find(int a) {
    //自己得先富贵了，真的找到真老大
    int zhenlaoda = a;
    while (laoda[zhenlaoda] != zhenlaoda) {
        zhenlaoda = laoda[zhenlaoda];
    }
    //什么都没有做，但是至少知道了真老大是谁，可以帮别人；
    int 每一次帮你的人 = a;
    while (每一次帮你的人 != zhenlaoda) {
        每一次帮你的人 = laoda[a];  // 记录爷爷的节点是谁
        laoda[a] = zhenlaoda;
        a = 每一次帮你的人;
    }
    return zhenlaoda;
}

public void union(int a, int b) {
    int alaoda = find(a);
    int blaoda = find(b);
    if (alaoda == blaoda) return;
    if (size[alaoda] >= size[blaoda]) {
        laoda[blaoda] = alaoda; //!!注意这里！！
        size[alaoda] += size[blaoda];
    }else {
        laoda[alaoda] = blaoda;
        size[blaoda] += size[alaoda];
    }
}

```



#### 其他版本，Pure Recursion Implementation

step1 : function 的定义

* int fnd(a): 给我一个点a可以找到a所在的帮派

step 2: base case

* laoda\[a] = a return a

step 3: subproblem

* find(laoda\[a]) 这个子问题return的结果的人其实就是zhenlaoda

step 4 recursion rule

* laoda\[a]上面的点已经路径压缩完了
* 真老大不就是子问题retun的结果了么？
* laoda\[a] = zhenlaoda
* return zhenlaoda

```java
//pure recursion
public int find(int a) {
    inf (laoda[a] == a) {
        return a;
    }
    int zhenlaoda = find(laoda[a]);
    laoda[a] = zhenlaoda;
    return zhenlaoda;
}

//更简化版本
public int find(int a) {
    return laoda[a] = a == laoda[a]? a: find(laoda[a]);
}
```

#### 面试简化版本

```java
class UnionFind{
    int[] laoda;
    public UnionFind(int n) {
        this.laoda = new int[n];
        for(int i = 0; i < n; i++) {
            laoda[i] = i;
        }
    
    }
    public int find(int a) {
        return laoda[a] = a == laoda[a]? a: find(laoda[a]);
    }
    
    public void union(int a , int b) {
        int alaoda = find(a);
        int blaoda = find(b)l
        if (alaoda = blaoda) return;
        if (size[alaoda] >= size[blaoda]) {
            laoda[blaoda] = alaoda;
            size[alaoda] += size[blaoda];
        }else {
            laoda[alaoda] = blaoda;
            size[blaoda] += size[alaoda];
        }
    }
}
```

#### 多加一个getMaxSetLaoda

```java
class UnionFind{
    int[] laoda;
    int[] size;
    public UnionFind(int n) {
        this.laoda = new int[n];
        this.size = new int[n];
        for(int i = 0; i < n; i++) {
            laoda[i] = i;
            size[i] = i;
        }
    }
    public int find(int a) {
        return laoda[a] = a == laoda[a]? a: find(laoda[a]);
    }
    
    public void union(int a , int b) {
        int alaoda = find(a);
        int blaoda = find(b)l
        if  realMaxLaoda = find(maxLaoda);
        
        
        if (size[alaoda] >= size[blaoda]) {
            laoda[blaoda] = alaoda;
            size[alaoda] += size[blaoda];
            if (size[alaoda] > size[realMaxLaoda]) {
                maxLaoda = alaoda;
            }
        }else {
            laoda[alaoda] = blaoda;
            size[blaoda] += size[alaoda];
            if (size[blaoda]> size[realMaxLaoda]) {
                maxLaoda = blaoda;
            }
        }
    }
    public int getMAxSetLaoda() {
        return maxLaoda;
    }
}
```



#### add a method findMax()

* add a method findMax() to the union-find data type so that findMax(i) returns the largest element in the connected component containing i.

```java
class UnionFind{
    int[] laoda;
    int[] size;
    int[] max;
    public UnionFind(int n) {
        this.laoda = new int[n];
        this.size = new int[n];
        this.max = new int[n];
        for(int i = 0; i < n; i++) {
            laoda[i] = i;
            size[i] = i;
            max[i] = i;
        }
    }
    public int find(int a) {
        return laoda[a] = a == laoda[a]? a: find(laoda[a]);
    }
    
    public void union(int a , int b) {
        int alaoda = find(a);
        int blaoda = find(b)l
        if  (alaoda == blaoda) return;
        
        
        if (size[alaoda] >= size[blaoda]) {
            laoda[blaoda] = alaoda;
            size[alaoda] += size[blaoda];
            max[alaoda] = Math.max(max[alaoda], max[blaoda]);
        }else {
            laoda[alaoda] = blaoda;
            size[blaoda] += size[alaoda];
            max[alaoda] = Math.max(max[alaoda], max[blaoda]);
        }
    }
    public int getMAxSetLaoda() {
        return maxLaoda;
    }
}
```

