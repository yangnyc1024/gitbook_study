# Networks Using Blocks (VGG)

* 与芯片设计中工程师从放置晶体管到逻辑元件再到逻辑块的过程类似，神经网络架构的设计也逐渐变得更加抽象。研究人员开始从单个神经元的角度思考问题，发展到整个层，现在又转向块，重复层的模式。
* 使用块的想法首先出现在牛津大学的[视觉几何组（visual geometry group）](http://www.robots.ox.ac.uk/\~vgg/)的_VGG网络_中。通过使用循环和子程序，可以很容易地在任何现代深度学习框架的代码中实现这些重复的架构。

#### VGG块

* review经典卷积神经网络的基本组成部分是下面的这个序列：
  * 带填充以保持分辨率的卷积层；
  * 非线性激活函数，如ReLU；
  * 汇聚层，如最大汇聚层。
* 一个VGG块与之类似，由一系列卷积层组成，后面再加上用于空间下采样的最大汇聚层。
* 在最初的VGG论文中 ([Simonyan and Zisserman, 2014](https://zh.d2l.ai/chapter\_references/zreferences.html#id153))，作者使用了带有$$3×3$$卷积核、填充为1（保持高度和宽度）的卷积层，和带有$$2×2$$汇聚窗口、步幅为2（每个块后的分辨率减半）的最大汇聚层。

#### &#x20;VGG网络

* 与AlexNet、LeNet一样，VGG网络可以分为两部分：第一部分主要由卷积层和汇聚层组成，第二部分由全连接层组成。
*   \


    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-05 at 3.18.39 PM.png" alt="" width="375"><figcaption></figcaption></figure>
* VGG神经网络连接 [图7.2.1](https://zh.d2l.ai/chapter\_convolutional-modern/vgg.html#fig-vgg)的几个VGG块（在`vgg_block`函数中定义）。其中有超参数变量`conv_arch`。该变量指定了每个VGG块里卷积层个数和输出通道数。全连接模块则与AlexNet中的相同。
