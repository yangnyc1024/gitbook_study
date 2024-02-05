# Network in Network(NiN)

* LeNet、AlexNet和VGG都有一个共同的设计模式：通过一系列的卷积层与汇聚层来提取空间结构特征；然后通过全连接层对特征的表征进行处理。 AlexNet和VGG对LeNet的改进主要在于如何扩大和加深这两个模块。
* 或者，可以想象在这个过程的早期使用全连接层。然而，如果使用了全连接层，可能会完全放弃表征的空间结构。 _网络中的网络_（_NiN_）提供了一个非常简单的解决方案：在每个像素的通道上分别使用多层感知机 ([Lin _et al._, 2013](https://zh.d2l.ai/chapter\_references/zreferences.html#id93))
