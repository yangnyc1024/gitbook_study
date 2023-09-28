# Question 2 Determine the number of bits that are different between two integers

有哪个操作，可以找到两个bit是不是一样

* bitwise XOR ^(不是power哈)



```java
// Some code
int numberOfDifferentBits(int a, int b) {
    int x = a ^ b;
    int count = 0;
    while (x != 0) {
        count += x& 1;
        x = x>>> 1; //右移，左侧补零
    }
}
```

follow up question: can we count ones even faster? O(log(number of bits))

* 你可以两两分组
* hamming\_weight

