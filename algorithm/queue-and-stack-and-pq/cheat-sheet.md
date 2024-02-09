# Cheat Sheet

```java

class Solution {
  public class Cell implements Comparable<Cell>{
      int x;
      int y;
      int cost;
      Cell (int x, int y, int cost) {
          this.x = x;
          this.y = y;
          this.cost = cost;
      }
      @Override
      public int hashCode() {
          int hashCode = this.x + 31;
          hashCode = hashCode * this.y + 31;
          return hashCode;
      }
      @Override
      public boolean equals(Object obj) {
          if (this == obj) return true;
          if (!obj instanceof Cell) {

                   return false;

           }
          Cell that = (Cell) obj;
          return this.x == that.x && this.y == that.y;
      }
      @Override
      public int compareTo(Cell that) {
          int result = Integer.compare(this.cost, that.cost);
          int result_x = Integer.compare(this.x, that.x);
          int result_y = Integer.compare(this.y, that.y);
          if (result == 0) {
              return result_x;
          }
          else if (result == 0 && result_x == 0) {
              return result_y;
          }
          return result;
      }
  }  // Integer.collections??  (s1, s2) -> s1.val - s2.val?




class Integer implements Comparable<Integer> {
    private int value;
    public Integer(int value){
        this.value = value;
    }
    @Override
    public int compareTo(Integer another) {
        if (this.value == another.value) {
            return 0;
        }
        return this.value < another.value? -1: 1;
    }
    @Override
    public int hashCode() {
        int hashCode = this.x  + 31;
    }
    
}


// 例子
public static void main(String[] args){
    Integer one = new Integer(1);
    Integer two = new Integer(2);
    System.out.println(one.compareTo(two));
}



PriortyQueue<MyInteger> maxHeap = 
new PriorityQueue<>((s1, s2) -> Integer.compare(s2.value, s1.value));


PriorityQueue<Integer> maxHeap = new PriorityQueue<Integer>(Collections.reverseOrder());
```
