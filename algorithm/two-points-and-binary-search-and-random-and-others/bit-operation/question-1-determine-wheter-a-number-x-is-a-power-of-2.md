# Question 1 determine wheter a number x is a power of 2

x is a power of 2 if and only if&#x20;

1. x‘s binary representation has exactly one bit set
2. x > 0



solution 1

```java
// Some code
boolean isPowerOfTwo(int x) {
    if (x < 0) return false;
    int count = 0;
    for (int i = 0; i < 32; i++) {
        // bit tester: extract the i-th bit from x
        count += (x >> i) & 1;
    }
    return (count == 1);
}
```

solution 2

```java
// Some code
boolean isPowerOfTwo(int x) {
    if (x < 0) return false;
    int count = 0;
    for (int i = 0; i < 32; i++) {
        count += x& 1;
        if (count > 1) return false;
        x = x >> 1;
    }
    return true;
}
```

