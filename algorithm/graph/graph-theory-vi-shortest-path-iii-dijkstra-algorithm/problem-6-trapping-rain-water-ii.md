# Problem 6 Trapping Rain Water II





这道题最坑的部分是，一个是高度，一个是它这个点的蓄水高度

* （普及）高度是给里面点的蓄水高度准备的
* 蓄水高度是根据周围的点的（普及高度）高度来说



关键点

* 普及高度，只可能升高，不可能变低
* 走的点是从最小的普及高度，
* 蓄水量 = max（普及高度 - 该点的高度，0）





generate 要做什么

* 计算neighbor的蓄水量
  * 蓄水量 = max（cur.普及高度 - cur.高度，0）
* update到neighbor为止的普及高度
  * <mark style="color:green;">cost 就是普及高度 ，所以neighbor.普及高度 = max (cur.普及高度， neighbor的高度) (since cur.普及高度>0) = cur.普及高度 + max(0， neighbor的高度 - cur.普及高度)</mark>
    * cost 就是普及高度
    * cost(开始的点（外围一圈最小点）， x.neighbor) = cost(开始的点， x) + cost (x, neighbor)
    * 所以edge上的weight应该是这玩意 max(0， neighbor的高度 - cur.普及高度)



```java
class Element implements Comparable<Element> {
    int x;
    int y;
    int pujiHeightl
    public Element(int x, int y, int pujiHeight) {
        this.x = x;
        this.y = y;
        this.pujiHeight = pujiHeight;
    }
    @Override
    public int compareTo(Element other) {
        return Integer.compare(this.pujiHeight, other.pujiHeight);
    }
}
private static final int[][] dirs = new int[][]{{-1, 0}, {1,0)}, {0, 1}, {0 , -1}}
public int trainRainWater;
```
