# Classes, objects and references

## 0 基本概念

<mark style="color:blue;">Student firstStudend</mark> <mark style="color:red;">= new</mark> <mark style="color:green;">Student("Tom")</mark>

* <mark style="color:blue;">Declaration</mark>
* <mark style="color:red;">Instantiation</mark>
* <mark style="color:green;">Initialization</mark>

**一个class里面还有什么？**

* field\&method状态和行为

问题：你的fields\&methods有一些前缀修饰，这些又是什么呢？

### 1. Static

* members (fields, methods, classes) belong to class, not object(instance).
* 这里就是表示属于class，而不是instance，不管你是对fields还是methods

#### 例子1——修饰变量

* 如果没有static，你每次出现新的instance，可以看到每次都需要new一个
* 但是如果有static，你就只能new关于class
* 注意：你可以操作instance关于static的fields，但是没有错

#### 例子2 ------修饰method

!\[Screen Shot 2022-02-05 at 9.11.43 PM]\(./Screen Shot 2022-02-05 at 9.11.43 PM.png)

* static cannot call non-static members
* 属于类就属于类的来用
  * 公家用公家，私人可以用公家和私人的

#### 例子？？:

没听清楚

#### 例子3——修饰class

* 修饰的class，属于里面的class

#### Class variable vs Instance variable/Class method？

### 2. Final

* Once assignment，cannot be changed

**例子1——修饰variable**

!\[Screen Shot 2022-02-05 at 9.21.46 PM]\(./Screen Shot 2022-02-05 at 9.21.46 PM.png)

#### 例子中的例子

* 第一个不行，girlFriend是reference，你不能修改这个纸条
  * 你的girl friend名片可以换，但是gf不能换
* 第二个可以，因为我final的是reference，但是没有final object
* 你的final没有什么大的权限，你final reference，不能完全final object

!\[Screen Shot 2022-02-05 at 9.27.28 PM]\(./Screen Shot 2022-02-05 at 9.27.28 PM.png)



####
