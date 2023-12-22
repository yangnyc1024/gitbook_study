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
        else {
            int abs = Math.abs(array[j]);
            if (i == 0) {
                result.add(array[j]);
                j++;
            } else {
                boolean flag = false;
                while (i > 0) { // 还有你要的行星
                    if (array[i - 1] < abs) {
                        i--;
                    }
                    else if (array[i - 1] == abs) {
                        i--;
                        break;
                    }
                    else  {
                        break;
                    }
                }
                // 1. 你最牛，肯定加。 2. 你遇到了跟你一样大的，不加，你还不如放方向的也不能加
                if (i == 0 && !flag) {
                    result.add(array[j]);
                }
                j++;
            }
        }
    }
    int[]
}
```

