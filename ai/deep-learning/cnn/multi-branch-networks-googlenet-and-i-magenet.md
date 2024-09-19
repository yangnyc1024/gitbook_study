# Multi-Branch Networks(GoogLeNet\&I mageNet)

## Multi-Branch Networks: GoogLeNet & Inception | 多分支网络：GoogLeNet 和 Inception

#### 1. **What is GoogLeNet? | 什么是 GoogLeNet？**

**GoogLeNet** (also known as **Inception v1**) is a deep convolutional neural network architecture introduced by researchers at Google in the 2014 paper _"Going Deeper with Convolutions"_. GoogLeNet was designed to improve the computational efficiency of deep learning models while maintaining high accuracy. The network introduced a novel **multi-branch structure**, where multiple convolution operations (with different filter sizes) are performed in parallel, which is known as the **Inception module**.\
**GoogLeNet**（也称为 **Inception v1**）是谷歌研究人员在 2014 年的论文《利用卷积构建更深的网络》中提出的深度卷积神经网络架构。GoogLeNet 的设计目标是提高深度学习模型的计算效率，同时保持高精度。该网络引入了一种新的**多分支结构**，即多个卷积操作（具有不同的滤波器大小）并行执行，称为**Inception 模块**。

#### 2. **The Inception Module | Inception 模块**

The core idea of the Inception module is to allow the network to decide **which filter size** (e.g., 1x1, 3x3, 5x5) is most appropriate for extracting features from a given input, and to compute multiple filters in parallel. This enables the network to capture different levels of detail and scale within the same layer.

**Inception Module Structure | Inception 模块的结构**

Each Inception module has several parallel branches:

1. **1x1 Convolution**: A simple 1x1 convolution used for dimensionality reduction and to capture local patterns.
2. **3x3 Convolution**: A 3x3 convolution that captures medium-sized features.
3. **5x5 Convolution**: A 5x5 convolution for larger receptive fields to capture more global patterns.
4. **Max Pooling**: A pooling layer for downsampling and feature aggregation.

After the parallel operations are performed, the outputs are concatenated along the depth (channels) dimension.\
每个 Inception 模块有多个并行分支：

1. **1x1 卷积**：一个简单的 1x1 卷积，用于降维并捕捉局部模式。
2. **3x3 卷积**：一个 3x3 卷积，用于捕捉中等大小的特征。
3. **5x5 卷积**：一个 5x5 卷积，用于更大的感受野以捕捉更全局的模式。
4. **最大池化**：一个池化层用于下采样和特征聚合。

执行并行操作后，将输出在深度（通道）维度上进行拼接。

**Example of Inception Module | Inception 模块示例**

For example, given an input feature map, an Inception module might apply:

* **1x1 convolution** with 64 filters,
* **3x3 convolution** with 128 filters,
* **5x5 convolution** with 32 filters,
* **3x3 max pooling** followed by a 1x1 convolution with 32 filters.

These feature maps are then concatenated, creating a more expressive feature representation.\
例如，给定一个输入特征图，一个 Inception 模块可能会应用：

* **1x1 卷积**，使用 64 个滤波器，
* **3x3 卷积**，使用 128 个滤波器，
* **5x5 卷积**，使用 32 个滤波器，
* **3x3 最大池化**，后接一个 1x1 卷积，使用 32 个滤波器。

这些特征图随后被拼接，生成更具表达力的特征表示。

#### 3. **GoogLeNet Architecture | GoogLeNet 的架构**

GoogLeNet consists of **22 layers** (including convolutional layers, pooling layers, and fully connected layers) and multiple Inception modules. Compared to earlier architectures like AlexNet and VGG, GoogLeNet is deeper but more computationally efficient due to the following innovations:

* **Inception Modules**: Multi-branch architecture allowing the model to use different filter sizes and pooling operations in parallel.
* **1x1 Convolutions for Dimensionality Reduction**: The use of 1x1 convolutions before 3x3 and 5x5 convolutions to reduce the number of input channels, reducing computational costs.
* **Global Average Pooling**: Replaces fully connected layers with global average pooling at the end of the network to further reduce the number of parameters.

GoogLeNet 由 **22 层** 组成（包括卷积层、池化层和全连接层），并包含多个 Inception 模块。与早期的架构（如 AlexNet 和 VGG）相比，GoogLeNet 更深但计算效率更高，其创新包括：

* **Inception 模块**：多分支架构允许模型并行使用不同的卷积核大小和池化操作。
* **1x1 卷积降维**：在 3x3 和 5x5 卷积之前使用 1x1 卷积来减少输入通道数，从而降低计算成本。
* **全局平均池化**：在网络末端用全局平均池化替代全连接层，进一步减少参数数量。

**Architecture Overview of GoogLeNet | GoogLeNet 的架构概述**

1. **Input Layer**: 224x224 RGB image.
2. **First Convolutional Layer**: 7x7 convolutions followed by max pooling.
3. **Second Convolutional Layer**: 3x3 convolutions followed by max pooling.
4. **Inception Modules**: Multiple Inception modules stacked to extract multi-scale features.
5. **Global Average Pooling**: Instead of fully connected layers, global average pooling is used.
6. **Output Layer**: A softmax layer to classify images into 1000 categories (ImageNet).

#### 4. **Key Innovations of GoogLeNet | GoogLeNet 的关键创新**

* **Multi-Branch Structure | 多分支结构**: By allowing the model to apply multiple convolutions in parallel, GoogLeNet can capture features at different scales, making the network more versatile and effective. **多分支结构**：通过允许模型并行应用多个卷积操作，GoogLeNet 能够在不同尺度上捕捉特征，使得网络更加多样化和有效。
* **1x1 Convolutions for Efficiency | 1x1 卷积提高效率**: The use of 1x1 convolutions significantly reduces the number of parameters by shrinking the input depth, which reduces computational cost without sacrificing performance. **1x1 卷积提高效率**：通过使用 1x1 卷积大幅减少参数数量，减少了输入深度，降低了计算成本，而不会牺牲性能。
* **Global Average Pooling | 全局平均池化**: Instead of traditional fully connected layers, GoogLeNet uses global average pooling to reduce the number of parameters and mitigate overfitting. **全局平均池化**：GoogLeNet 使用全局平均池化代替传统的全连接层，减少了参数数量并缓解了过拟合问题。

#### 5. **Performance on ImageNet | 在 ImageNet 上的表现**

GoogLeNet achieved a **top-5 error rate of 6.7%** in the 2014 ImageNet Large Scale Visual Recognition Challenge (ILSVRC), which was a significant improvement over previous models like AlexNet and VGG. The multi-branch structure and efficient design allowed it to be deeper while using fewer parameters than comparable architectures.\
GoogLeNet 在 2014 年的 ImageNet 大规模视觉识别挑战赛（ILSVRC）中取得了 **6.7% 的 top-5 错误率**，这是对 AlexNet 和 VGG 等先前模型的显著改进。多分支结构和高效设计使其在使用比其他架构更少参数的同时实现了更大的深度。

#### 6. **Why Use GoogLeNet? | 为什么使用 GoogLeNet？**

* **Efficient Yet Deep | 高效且深度**: GoogLeNet strikes a balance between depth and computational efficiency. It uses fewer parameters than VGG but achieves higher accuracy, thanks to the Inception modules. **高效且深度**：GoogLeNet 在深度和计算效率之间达到了平衡。它使用的参数比 VGG 少，但由于 Inception 模块，能够实现更高的精度。
* **Multi-Scale Feature Extraction | 多尺度特征提取**: The Inception module allows GoogLeNet to capture features at different scales simultaneously, making it effective for diverse image recognition tasks. **多尺度特征提取**：Inception 模块使 GoogLeNet 能够同时捕捉不同尺度的特征，这使其在各种图像识别任务中表现出色。
* **Reduced Overfitting | 减少过拟合**: By using global average pooling and avoiding fully connected layers, GoogLeNet reduces the risk of overfitting and makes the model more generalizable. **减少过拟合**：通过使用全局平均池化并避免全连接层，GoogLeNet 减少了过拟合的风险，使得模型具有更好的泛化能力。

#### 7. **Limitations of GoogLeNet | GoogLeNet 的局限性**

* **Complex Architecture | 复杂的架构**: Although GoogLeNet is efficient, its architecture is more complex than simpler models like AlexNet or VGG, making it harder to implement and optimize. **复杂的架构**：尽管 GoogLeNet 高效，但其架构比 AlexNet 或 VGG 更复杂，使得实现和优化更加困难。
* **Inception Module Complexity | Inception 模块的复杂性**: The multi-branch Inception module introduces more parallel operations, which can increase the computational and memory requirements, especially during training. **Inception 模块的复杂性**：多分支的 Inception 模块引入了更多并行操作，可能增加训练期间的计算和内存需求。

#### 8. **Example of GoogLeNet in Action | GoogLeNet 的操作示例**

Imagine using GoogLeNet to classify an image of a bird. The input image (224x224 RGB) is processed through several Inception modules:

1. **Early Layers**: The first layers detect simple features like edges.
2. **Inception Modules**: The Inception modules capture multi-scale features, such as the shape of the bird’s wings or the texture of its feathers.
3. **Global Average Pooling**: Aggregates the learned features across the entire image.
4. **Output Layer**: The network predicts the bird's species with a high confidence score.

In this case, GoogLeNet’s ability to capture features at different scales enables it to identify the bird accurately.\
想象使用 GoogLeNet 对鸟的图像进行分类。输入图像（224x224 RGB）通过多个 Inception 模块处理：

1. **早期层**：前几层检测简单的特征，如边缘。
2. **Inception 模块**：Inception 模块捕捉多尺度特征，例如鸟翼的形状或羽毛的纹理。
3. **全局平均池化**：聚合整个图像中学习到的特征。
4. **输出层**：网络以较高的置信度预测鸟的种类。

在这种情况下，GoogLeNet 捕捉不同尺度的特征的能力使其能够准确识别鸟类。



GoogLeNet 引入了 **Inception 模块**，这是一个并行应用不同卷积核大小的多分支结构。它使用 **1x1 卷积** 来降维，并使用 **全局平均池化** 代替全连接层。优点是高效、深度、能够捕捉多尺度特征，缺点是比早期的架构（如 AlexNet 和 VGG）更复杂。

## Extra Reading

* 在2014年的ImageNet图像识别挑战赛中，一个名叫_GoogLeNet_ ([Szegedy _et al._, 2015](https://zh.d2l.ai/chapter\_references/zreferences.html#id162))的网络架构大放异彩。 GoogLeNet吸收了NiN中串联网络的思想，并在此基础上做了改进。&#x20;
* 这篇论文的一个重点是解决了什么样大小的卷积核最合适的问题。 毕竟，以前流行的网络使用小到$$1×1$$，大到$$11×11$$的卷积核。 本文的一个观点是，有时使用不同大小的卷积核组合是有利的。

#### Inception 块

* 在GoogLeNet中，基本的卷积块被称为_Inception块_（Inception block）。这很可能得名于电影《盗梦空间》（Inception），因为电影中的一句话“我们需要走得更深”（“We need to go deeper”）。
*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-05 at 3.07.24 PM.png" alt=""><figcaption></figcaption></figure>

#### GoogleLeNet模型

* GoogLeNet一共使用9个Inception块和全局平均汇聚层的堆叠来生成其估计值。Inception块之间的最大汇聚层可降低维度。 第一个模块类似于AlexNet和LeNet，Inception块的组合从VGG继承，全局平均汇聚层避免了在最后使用全连接层。
* 第一个模块使用64个通道、$$7×7$$卷积层。
* 第二个模块使用两个卷积层
  * 第一个卷积层是64个通道、$$1×1$$卷积层；第二个卷积层使用将通道数量增加三倍的$$3×3$$卷积层。 这对应于Inception块中的第二条路径。
* 第三个模块串联两个完整的Inception块。&#x20;
  * 第一个Inception块的输出通道数为$$64+128+32+32=256$$，四个路径之间的输出通道数量比为$$64:128:32:32=2:4:1:1$$。 第二个和第三个路径首先将输入通道的数量分别减少到$$96/192=1/2$$和$$16/192=1/12$$，然后连接第二个卷积层。
  * 第二个Inception块的输出通道数增加到$$128+192+96+64=480$$，四个路径之间的输出通道数量比为$$128:192:96:64=4:6:3:2$$。 第二条和第三条路径首先将输入通道的数量分别减少到$$128/256=1/2$$和$$32/256=1/8$$。
* 第四模块更加复杂， 它串联了5个Inception块，
  * 其输出通道数分别是$$192+208+48+64=512$$、$$160+224+64+64=512$$、$$128+256+64+64=512$$、$$112+288+64+64=528$$和$$256+320+128+128=832$$。



* &#x20;GoogLeNet吸收了NiN中串联网络的思想，并在此基础上做了改进。 这篇论文的一个重点是解决了什么样大小的卷积核最合适的问题。 毕竟，以前流行的网络使用小到$$1×1$$，大到$$11×11$$的卷积核。
* d2l的一个观点是，有时使用不同大小的卷积核组合是有利的。



#### Inception块

* 在GoogLeNet中，基本的卷积块被称为_Inception块_（Inception block）。这很可能得名于电影《盗梦空间》（Inception），因为电影中的一句话“我们需要走得更深”（“We need to go deeper”）。

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-05 at 3.24.22 PM.png" alt="" width="375"><figcaption></figcaption></figure>

* Inception块由四条并行路径组成。 前三条路径使用窗口大小为$$1×1$$、$$3×3$$和$$5×5$$的卷积层，从不同空间大小中提取信息。 中间的两条路径在输入上执行$$1×1$$卷积，以减少通道数，从而降低模型的复杂性。 第四条路径使用$$3×3$$最大汇聚层，然后使用$$1×1$$卷积层来改变通道数。
* 这四条路径都使用合适的填充来使输入与输出的高和宽一致，最后我们将每条线路的输出在通道维度上连结，并构成Inception块的输出。在Inception块中，通常调整的超参数是每层输出通道数。
* 那么为什么GoogLeNet这个网络如此有效呢？ 首先我们考虑一下滤波器（filter）的组合，它们可以用各种滤波器尺寸探索图像，这意味着不同大小的滤波器可以有效地识别不同范围的图像细节。 同时，我们可以为不同的滤波器分配不同数量的参数。

#### GoogleLeNet模型

* GoogLeNet一共使用9个Inception块和全局平均汇聚层的堆叠来生成其估计值。Inception块之间的最大汇聚层可降低维度。 第一个模块类似于AlexNet和LeNet，Inception块的组合从VGG继承，全局平均汇聚层避免了在最后使用全连接层。
*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-05 at 3.25.31 PM.png" alt="" width="179"><figcaption></figcaption></figure>
* 我们逐一实现GoogLeNet的每个模块。
  * 第一个模块使用64个通道、$$7×7$$卷积层。
  * 第二个模块使用两个卷积层：第一个卷积层是64个通道、$$1×1$$卷积层；第二个卷积层使用将通道数量增加三倍的$$3×3$$卷积层。 这对应于Inception块中的第二条路径。
  * 第三个模块串联两个完整的Inception块。&#x20;
    * 第一个Inception块的输出通道数为$$64+128+32+32=256$$，四个路径之间的输出通道数量比为$$64:128:32:32=2:4:1:1$$。
    * &#x20;第二个和第三个路径首先将输入通道的数量分别减少到$$96/192=1/2$$和$$16/192=1/12$$，然后连接第二个卷积层。第二个Inception块的输出通道数增加到$$128+192+96+64=480$$，四个路径之间的输出通道数量比为$$128:192:96:64=4:6:3:2$$。&#x20;
    * 第二条和第三条路径首先将输入通道的数量分别减少到$$128/256=1/2$$和$$32/256=1/8$$。
  * 第四模块更加复杂， 它串联了5个Inception块，其
    * 输出通道数分别是$$192+208+48+64=512$$、$$160+224+64+64=512$$、$$128+256+64+64=512$$、$$112+288+64+64=528$$和$$256+320+128+128=832$$。 这些路径的通道数分配和第三模块中的类似，首先是含$$3×3$$卷积层的第二条路径输出最多通道，其次是仅含$$1×1$$卷积层的第一条路径，之后是含$$5×5$$卷积层的第三条路径和含$$3×3$$最大汇聚层的第四条路径。 其中第二、第三条路径都会先按比例减小通道数。 这些比例在各个Inception块中都略有不同。
  * 第五模块包含输出通道数为$$256+320+128+128=832$$和$$384+384+128+128=1024$$的两个Inception块。&#x20;
    * 其中每条路径通道数的分配思路和第三、第四模块中的一致，只是在具体数值上有所不同。 需要注意的是，第五模块的后面紧跟输出层，该模块同NiN一样使用全局平均汇聚层，将每个通道的高和宽变成1。 最后我们将输出变成二维数组，再接上一个输出个数为标签类别数的全连接层。
  * GoogLeNet将多个设计精细的Inception块与其他层（卷积层、全连接层）串联起来。其中Inception块的通道数分配之比是在ImageNet数据集上通过大量的实验得来的。
  * GoogLeNet和它的后继者们一度是ImageNet上最有效的模型之一：它以较低的计算复杂度提供了类似的测试精度。
