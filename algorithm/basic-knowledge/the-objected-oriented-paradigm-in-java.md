# The objected-oriented paradigm in java



* **所有的计算机都是data+operation**

#### Basic concept---- Object

* class：蓝图
* object/instance：
* reference
  * 就是名片
* dereferencing
  * 就是用名片去看看
  * 那个‘点’array.length就是dereference， array\[]也是dereference

/

#### Primitive types vs Class types

**那刚才我们介绍object完了，我们介绍什么？**

* 所有的都是object，除了八种primitive types

**你怎么创造新的呢**？

* 操作new会有以下反应：
  * Declaration
  * Instantiation： firstStudent = new Student (...)
  * Initialization

#### Working with Objects

#### Object memory layout

具体操作，这个挖掘机存在哪里呢？

* stack(栈)
  * instance中的local primitive variable在method里面，就存在着里面
  * instance中的local object reference stores
* heap(推)
  * instance中的你new出来的object就在这里
  * store fields？

!\[Screen Shot 2022-02-05 at 8.31.36 PM]\(./Screen Shot 2022-02-05 at 8.31.36 PM.png)

**Example 1**

注意

!\[Screen Shot 2022-02-05 at 8.34.09 PM]\(./Screen Shot 2022-02-05 at 8.34.09 PM.png)

注意注意命名方式！！！！

* public 是全大写开头
* field 开头是lowerCamel

**Example2:**

!\[Screen Shot 2022-02-05 at 8.28.43 PM]\(./Screen Shot 2022-02-05 at 8.28.43 PM.png)

* 你的fields variable里面都是object呀，不管是primitive还是object，都是object，只是不同类型的object

#### Default Value/ Constructor, this, and Null pointers

* 注意constructor
  * 不需要返回值，
  * 注意里面的this的使用
  * 注意parameter list
* default：zero/false/null，这是针对field，但是不是针对local variable（在method里面）

