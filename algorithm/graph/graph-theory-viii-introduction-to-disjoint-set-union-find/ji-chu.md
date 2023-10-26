# 基础

#### 第四种Union-FInd: Weighted Union FInd with PathCompression

Path Compression：路径压缩

路径压缩精髓：苟富贵勿相忘(一个人富贵了，所有帮助给你的人全都浮过)



```java
//细节版本
public int find(int a) {
    //自己得先富贵了，真的找到真老大
    int zhenlaoda = a;
    while (laoda[zhenlaoda] !=. zhenlaoda) {
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

