# Extra: Multiple Input and Multiple Output Channels

#### Channel

* 当我们添加通道时，我们的输入和隐藏的表示都变成了三维张量。例如，每个RGB输入图像具有$$3\times h \times w$$的形状。我们将这个大小为$$3$$的轴称&#x4E3A;_&#x901A;道_（channel）维度。本节将更深入地研究具有多输入和多输出通道的卷积核。
* 用$$c_i$$和$$c_0$$分别表示输入和输出通道的数目，并让$$k_h$$和$$k_w$$为卷积核的高度和宽度。为了获得多个通道的输出，我们可以为每个输出通道创建一个形状为$$c_i \times k_h \times k_w$$的卷积核张量，这样卷积核的形状是$$c_o \times c_i \times k_h \times k_w$$。在互相关运算中，每个输出通道先获取所有输入通道，再以对应该输出通道的卷积核计算出结果。
