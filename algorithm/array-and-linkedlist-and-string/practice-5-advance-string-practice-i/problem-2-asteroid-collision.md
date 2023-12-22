# Problem 2 Asteroid Collision





High Level: 每颗行星，尝试撞

Case 1: 正方向==》 model as left, keep ==> store it in stack

* 正向最后保留的星星其实应该是开放的做括号==》 stack里==> i左边不包含i的部分

Case2: 负方向==〉 model as right

* case 2.1 never seen a left before
  * 直接把这个行星进result==》 本质上是上一道题的非法右括号
* case 2.2 遇到过正向飞的小行星
  * 比大小
    * 负方向大：爆炸---pop--不要正向
    * 正方向大：不要现在的
    * 一样大：来的不要的，还得掏出来一个



* 先加往左飞的，通过当场记录，就像你发现违规的右括号
* 然后再从index开始把向右飞的加进去

```java
public int[] collision(int[] array) {
    List<Integer> result = new ArrayList<>();
    // assume array valid
    int i = 0;
    int j = 0;
    while (j < array.length) {
        if (array[j] > 0) {. // 向右飞的
            array[i] = array[j];
            i++;
            j++;
        }
        else { //向左飞的（没全部炸掉全部炸掉？）
            int abs = Math.abs(array[j]);
            if (i == 0) { // 假设你是第一个向左飞的
                result.add(array[j]);
                j++;
            } else {
                boolean flag = false;
                while (i > 0) { // 这颗向左的行星，一直可以消灭
                    if (array[i - 1] < abs) { 
                        i--;
                    }
                    else if (array[i - 1] == abs) {
                        i--;
                        flag = true;
                        break;
                    }
                    else  { //一个都炸不了
                        break;
                    }
                }
                // 1. 你最牛，肯定加。 2. 你遇到了跟你一样大的，不加，你还不如放方向的也不能加
                if (i == 0 && !flag) { //你没有同归于尽
                    result.add(array[j]);
                }
                j++;
            }
        }
    }
    //最有应该一共剩多少颗行星，往左飞：result.size(), 往右飞:i
    int[] resultArray = new int[result.size() + i];
    int index = 0;
    for (Integer element: result) {
        resultArray[index] = element;
        index++;
    }
    for (int k = 0; k < i ; k++) {
        resultArray[index] = array[k];
        index++
    }
    return resultArray;
}
```

