# Question 4 Array Hopper I

#### Method 1 DP 从后往前跳

Step 1: DP definition

* dp\[i] represent from current index i could reach last index or not

Step 2: base case

* dp\[array.length - 1] = True

Step 3: Induction Rule

* 从当前点跳
* 从这点往后找一点可以跳的跳
*   dp\[i] = true iff i + array\[i] >= length -1

    * or exist an j such that dp\[j] = true, i + array\[i] >= j



```java
public class Solution {
  public boolean canJump(int[] array) {
    // Write your solution here
    // sanity check
    if (array.length == 1) {
      return true;
    }
    boolean[] canJump = new boolean[array.length];
    canJump[array.length - 1] = true;
    for (int i = array.length - 2; i >= 0; i--) {
      if (i + array[i] >= array.length - 1){// case 1:表示你直接就可以跳，所以不需要回头看了
        canJump[i] = true;
      } else {
        for (int j = 1; j <= array[i]; j++) {
          if (canJump[i + j] && i + array[i] >= j) {
            canJump[i] = true;
            break; // 因为已经找到了 不需要找了
          }
        }
      }
    }
    return canJump[0];
  }
}
```

#### Method 2 DP 从前往后跳

Step1 DP 定义

* dp\[i] represent from index 0, could reach the ending index i or not

Step2 Base Case

* dp\[0] = true

Step 3 Induction Rule

* 从0能不能跳到我这里？
  * case 1:  从0一步就可以跳到我这里
  * case 2: 要不从0开始找，找到一个可以跳到我这里的
* dp\[i] = true iff&#x20;
  * array\[0] >= i or exist an j such that j + array\[j] >= i && dp\[j ] = true for any j < i



```java
public class Solution {
  public boolean canJump(int[] array) {
    // Write your solution here
    // sanity check
    if (array.length == 1) {
      return true;
    }
    boolean[] dp = new boolean[array.length];
    dp[0] = true;
    for (int i = 1; i < array.length; i++) {// linear scan 所有的ending index i
      if (array[0] >= i) {  // case 1: 不用look back直接到就行了
        dp[i] = true;
      } else {
        for (int j = 0; j < i; j++) { // case 2: 自己到不了，后头看所有可能的中继点
          if (dp[j] && j + array[j] >= i) {
            dp[i] = true;
            break;
          }
        }
      }
    }
    return dp[array.length - 1];
  }
}

```
