# Problem 7 Add two Polynomial

注意：

* power不一样的情况
* power不一定从大到小

```java
public class PolyNode {
    public int coefficient;
    public int power;
    public PolyNode
}
PolyNode AddPoly(PolyNode p1, PolyNode p2) {
    PolyNode dummy = new PolyNode();
    PolyNode cur = dummy;
    
    while (p1 != null || p2!= null) { 
        // Clarify: power都是正的
        int e1 = p1 == null? -1: p1.power;
        int e2 = p2 == null? -1: p2.power;
        if (e1 > e2) {
            cur.next = new PolyNode(p1.cofficient, p1.power);
            p1 = p1.next;
            cur = cur.next;
        }else if (e1 < e2) {
            cur.next = new PolyNode(p2.cofficient, p2.power);
            p2 = p2.next;
            cur = cur.next;
        }else {
            if (p1.coefficient + p2.coofficient != 0) {
                cur.next = new PolyNode (p1.coeffieient + p2.coefficient, p1.power);
                cur = cur.next;
            }
            p1 = p1.next;
            p2 = p2.next;
        }
    }

}
```
