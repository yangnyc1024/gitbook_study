# Question 2 Iterator for Combination

### Method 1

#### 和刚才的题目一样

* 只不过字母不一定连续，但是保证了顺序是递增的

#### 总结

* Case 1: 已经处理完所有的位置，收集solution，减1把数字++
  * 尝试把能的最后一位递增到原始given str中的下一位
* Case 2:这个书自己超过了最大范围说明当前不合法必须回退到前一位
  * 最大范围：这三位启示最大的就是原始given str中倒叙的后K位
  * 对于查找谁是那个所谓的最高可以增大的位：倒叙遍历第一个不同的
  * 最后一位找到了，他会变大成为谁呢？
* Case 3:顺水推舟直到所有数字都递增
  * 这一位以及这一位以后的所有字母都照搬given str



有一些浪费时间的String operation/use case

* substring
* indexOf



```java
// Some code
class CombinationIterator {
    char[] current;
    String orignalStr;
    boolean hasNext;
    public CombinationIterator(String characters, int combinationLength) {
        this.current = characters.substring(0,combinationLength).toCharArray();
        this.originalStr = characters;
        hasNext = true; // 注意CART
    
    }

    public String next(){
        if (!hasNext) {
            return "";
        }
        String result = new String(current);
        
        int i = current.length - 1;
        int j = originalStr.length() - 1;
        while (i >= 0 && current[i] == originalStr.charAt(j)) {
            i--;
            j--;
        }
        if (i == -1) {
            hasNext = false; // 没办法变化了
        } else {
            int index = priginalStr.indexOf(current[i]);
            for (int k = i; k < current.length; k++) {
                index++;
                current[k] = originalStr.charAt(index);
            }
        
        }
        return result;
    }


    public boolean hasNext(){
        return this.hasNext;
    }
}
```





### Method 2 看use case的情况：需要连续的情况下不真的连续--》 bit mask(bit operation)



bitmask: 我用一个数字代表我的选择

bit：要么0代表不选，要么1代表选（一个位置上，几个进制代表几个状态）

abcd：选与不选这些字母的问题其实就是这四位的数字里哪些是1，哪些是0





易错点

* 最小的mask是谁？最小的size combination 0011(cd)
* 开始的mask怎么做出来的呢？
  * ab --》 1100
* 一开始最小的combination = (1 << totalLength) - (1 << (totalLength - combinationLength))

```java
// Some code

class CombinationIterator {
    private int combinationLength;
    private String originalStr;
    private int totalLength;
    private int minBitmask;
    private int bitmask; //current
    private boolean foundNext;
    
    public CombinationIterator(String characters, int combinationLength) {
        this.orginalStr = character;
        this.combinationLength = combinationLength;
        this.totalLength = characters.length();
        this.bitmask = (1 << totalLength) - (1 << (totalLength - combinationLength));
        this.foundNext = true;
        this.minBitmask = (1 << comibinationLength) - 1;
    
    }
    public String next(){
        if (!hasNext()) {
            return "";
        }
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < totalLength; i++) {
            if ((bitmask & (1 << totalLength - 1 - i) != 0)) {
                sb.append(originalStr.charAt(i));
            }
        }
        foundNext = false;
        return sb.toString();
    }
    
    public boolean hasNext(){
        if (foundNext) {
            return true;
        }
        if (bitmask < minBitmask) {
            return false;
        }
        bitmask --;
        while (bitmask >= minBitmask && Integer.bitCount(bitmask) != combinationLength) {
            bitmask--;
        }
        foundNext = bitmask >= minBitmask;
        return foundNext;
    }

}
```





API logic:

* get next maskNumber:
  * 能直接把currentmask 减1
    * 1100（ab） - 1 = 1011(acd)
    * 1011(acd) - 1= 1010(ac)
  * 算法：逐次减1，直到得到hamming weight 和combinationLength一样的第一个mask
* 如何对应上Mask和String：bitGetter 把对应位是1的位填补位originalStr中对应character对于第i个index，是否要把它加到现在的current result里
  * （currentMask & (1 << n - 1 - i)）!= 0





### Side Problem 1: Number of 1Bits

Method 1: Java Library:&#x20;

* return Integer.bitCount(n);

Method 2: 自己实现

```java
// Some code
int count = 0;
while (n != 0) {
    count += (n & 1);
    n >>> 1;

}
return count;
```

Method 3：技巧

```java
// Some code

int count = 0;
while (n! = 0) {
     n = n & (n - 1);
     count++;
}
return count;
```

竞赛技巧： n& (n - 1)是什么意思

* 把n的二进制表示中最低的上的1改成0
* example
  * n = 0b10100, n-1 = 0b10011&#x20;
  * n & n-1 = 0b10000
* example: 判断一个数字是不是2的幂次方
  * return n > 0 && (n & (n - 1) == 0)

### Side Problem 2: Hamming Distance

本质上就是异或之后的数字中的hamming weight是多少



```java
// Some code

public int hammingDistance(int x, int y) {
    int number = x ^ y;
    int count = 0;
    while (number != 0) {
        number = number & (number - 1);
        count++;
    }
    return distance;
}
```
