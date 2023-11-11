---
description: Random
---

# Class Random

#### 知识点1:  java.lang.Math.random

* Math.random() 能够返回带正号的double值，该值\[0,1)



#### 知识点2: java.util.Random

```java
Random random1 = new Random();
random1.nextInt(10)

Random random2 = new Random(20);
```

* 默认当前系统时间的毫秒数作为种子数生成\[0,10）内随机整数序列
* 或者指定种子

<figure><img src="../../.gitbook/assets/Screenshot 2023-07-19 at 7.47.38 PM.png" alt=""><figcaption></figcaption></figure>

#### Summary



```java
Random random = new Random();

//生成[a, b)?区间的整数
int randomNumber = random.nextInt(b - a + 1) + a;
double randomNumber = Math.random() * (b -a) + a;

//生成[1, 2.5)区间的小数
double d3 = random.nextDouble() * 1.5 + 1; //本来是[0,1)


//生成-2^31到 2^31-1区间的整数
int n = random.nextInt();

```
