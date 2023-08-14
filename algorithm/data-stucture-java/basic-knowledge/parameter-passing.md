# Parameter passing

####

Java： always pass by value(primitive type pass primitive value, object type pass its reference)

example:



#### 题目1

所有定义在method里的变量: local variable, 局部变量一定存在Stack里

stack: b, x1, a1, x3

heap:  x2, a2, x

```java
public class Main{
    public static void main(String[] args) {
        B b = new B();
        b.f();
        b.a2.g(5);
    }
}
class B {
    public void f(){
        int x1 = 7;
        A a1 = new A();
    }
    int x2 = 8;
    A a2 = new A();
}
class A {
    int x = 7;
    public void g(int num) {
        int x3 = num;
        System.out.print(x3);
    }

}
```

#### 题目2

