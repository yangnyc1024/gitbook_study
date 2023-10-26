# Priority Queue小练习

```java
class MyNode {
    int A;
    String B;
    char C;
    int D;
    long E;
    short F;
    boolean G;
}


```

规则：

* 先比较A，谁小谁优先
* A一样比B，B字母序列谁大谁优先，B一样大的时候，B的长度越短越优先，都一样的话
* 都一样的话比较C，C离char “a” asc码越近越优先
* 不然比D和E相加的结果（默认不会超界），相加的结果越大越优先，
* 不然我们比F，F越小越优先
* 如果前面都一样，比G，true优先，如果到这都一样，这两Node一样优先

不合理的地方：

* B字母序列谁大谁优先，B一样大的时候，B的长度越短越优先
* 字母序一样的时候，长度一样是一样的，找不到字母序列，长度不一样的case



```java
class MyNode {
    int A;
    String B;
    char C;
    int D;
    long E;
    short F;
    boolean G;
    public MyNode(int A, String B, char C, int D, long E, short F, boolean G) {
        this.A = A;
        this.B = B;
        this.C = C;
        this.D = D;
        this.E = E;
        this.F = F;
        this.G = G;
    }
    class MyComparator implememnts Comparator<MyNode> {
        @Override
        public int compare(MyNode node1, MyNode node2) {
            if (node1.A < node2.A) {
                return -1;
            } else if (node1.A > node2.A) {
                return 1;
            } else { // node1.A == node2.A
                if (node1.B.compareTo(node2.B) == -1) {
                    return 1;
                }
                else if (node1.B.compareTo(node2.B) == 1) {
                    return -1;
                }else{ // node1.B.length() == node2.B.length()
                    if (node1.C - 'a' < node2.C - 'a') {
                        return -1;
                    } else if (node1.C - 'a' > node.C - 'a') {
                        return 1;
                    } else { // node1.C - 'a' == node2.C - 'a'
                        if ((long)node1.D + node1.E > (long)node2.D + node2.E) {
                            return -1;
                        } else if ((long)node1.D + node1.E < (long)node2.D + node2.E){
                            return 1
                        } else {// (long)node1.D + node1.E == (long)node2.D + node2.E
                            if (node1.F < node2.F) {
                                return -1;
                            } else if (node1.F > node2.F) {
                                return 1;
                            } else { // node1.F == node2.F
                                if (node1.G = node2.G) {
                                    return 0;
                                } else if (node1.G){ 
                                    return -1;
                                } else {
                                    return 1;
                                }
                            }
                        
                        }
                    
                    }
                }
                
            }
        
        } 
    }
}

public static void main(String[] args) {
    List<MyNode> nodes = new ArrayList<>();
    MyNode node1 = new MyNode(2, "Harryyyds", 'z', 100, 10000000000L, (short)90, true);
    MyNode node2 = new MyNode(2, "Harry", 'a', 2, 10000000000L, (short)100, true);
    MyNode node3 = new MyNode(1, "Harry", 'a', 2, 10000000000L, (short)100, true);
    MyNode node4 = new MyNode(2, "Harryyyds", 'z', 2, 10000000000L, (short)100, true);
    MyNode node5 = new MyNode(2, "Harryyyds", 'z', 100, 10000000000L, (short)90, false);
    MyNode node6 = new MyNode(2, "Harryyyds", 'a', 2, 100000L, (short)100, true);
    MyNode node7 = new MyNode(2, "Harryyyds", 'z', 100, 10000000000L, (short)90, true);
    MyNode node8 = new MyNode(2, "Harryyyds", 'z', 100, 10000000000L, (short)100, true);
    MyNode node9 = new MyNode(2, "Harryyyds", 'z', 100, 10000000000L, (short)80, false);
    nodes.add(node1);
    nodes.add(node2);
    nodes.add(node3);
    nodes.add(node4);
    nodes.add(node5);
    nodes.add(node6);
    nodes.add(node7);
    nodes.add(node8);
    nodes.add(node9);
    for (int i = 0 ; i < nodes.size(); i++) {
        System.out.println("Before Sorting:" + nodes.get(i).A + " " + nodes.get(i).B + " "
                 + nodes.get(i).C + " " + nodes.get(i).D + " " + nodes.get(i).E + " "
                 + nodes.get(i).F + " " + nodes.get(i).G)
    }
    Collections.sort(nodes, new MyComparator());
    for (int i = 0 ; i < nodes.size(); i++) {
        System.out.println("After Sorting:" + nodes.get(i).A + " " + nodes.get(i).B + " "
                 + nodes.get(i).C + " " + nodes.get(i).D + " " + nodes.get(i).E + " "
                 + nodes.get(i).F + " " + nodes.get(i).G)
    }   
}

```
