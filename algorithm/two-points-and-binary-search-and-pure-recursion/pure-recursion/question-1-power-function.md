# Question 1 Power Function



SC& TC: O(n), O(1)

```java
public int power(int a, int b) {
    // step 1 function, input a, b, output a^b
    // step 2 base case
    if (b == 0) {
        return 1;
    }
    // step 3 subproblem
    int ret = power(a, b -1);
    // step 4 recursive rule
    return a * ret;
}


public int power(int a, int b) {
    // step 1 function, input a, b, output a^b
    // step 2 base case
    //if (b == 0 || a == 1) {
    //    return 1;
    //}
    //if (b == 1 || a == 0) {
    //    return a;
    //}
    if (b == 0) {
        return 1;
    }
    ret = power(a, b /2);
    // step 3 subproblem
    if (b % 2 == 0) {
        return ret * ret;
    }
    return ret * ret * b;
    // step 4 recursive rule
}
```

如果有负数？

```java

public int power(int a, int b) {
    // step 1 function, input a, b, output a^b
    // step 2 base case
    //if (b == 0 || a == 1) {
    //    return 1;
    //}
    //if (b == 1 || a == 0) {
    //    return a;
    //}
    if (b == 0) {
        return 1;
    }
    if (b < 0) {
        return 1/poer(a, -(b + 1) * a);
    }
    ret = power(a, b /2);
    // step 3 subproblem
    if (b % 2 == 0) {
        return ret * ret;
    }
    return ret * ret * b;
    // step 4 recursive rule
}
```





如果我要算a的b次方，b一定可以表示成为log2(n) +1 个二进制位

* 13 = 1 \* 2^3  + 1 \* 2^2 + 0^ 2^0 +&#x20;
* a^n = a^(n的二次方表达)
