# Densely Connected Networks(DenseNet)

### Densely Connected Networks (DenseNet) | 密集连接网络 (DenseNet)

#### 1. **What is DenseNet? | 什么是 DenseNet？**

**DenseNet** is a convolutional neural network (CNN) architecture introduced by Gao Huang, Zhuang Liu, Laurens van der Maaten, and Kilian Q. Weinberger in their 2017 paper titled _"Densely Connected Convolutional Networks."_ The key idea behind DenseNet is to introduce **dense connections** between layers, meaning that **each layer receives input from all previous layers** and passes its feature maps to all subsequent layers.\
**DenseNet** 是一种卷积神经网络（CNN）架构，由 Gao Huang、Zhuang Liu、Laurens van der Maaten 和 Kilian Q. Weinberger 在 2017 年的论文《密集连接卷积网络》中提出。DenseNet 的核心思想是引入 **密集连接**，即**每一层的输入来自所有先前层的输出**，并将其特征图传递给所有后续层。

#### 2. **How DenseNet Works? | DenseNet 是如何工作的？**

In DenseNet, each layer is connected to every other layer in a **feed-forward** manner. Instead of summing the outputs like in ResNet, DenseNet **concatenates** the outputs of the previous layers as the input to the next layer. This ensures that each layer has **direct access to the gradients** from the loss function and the **original input**, which improves the flow of information and gradients through the network.

**Dense Block | 密集块**

The core component of DenseNet is the **dense block**, where all layers are connected to each other. Each dense block consists of multiple convolutional layers, and each layer takes the concatenated output of all previous layers as its input.

For example, in a dense block with layers $$L_0, L_1, L_2, \dots, L_n$$:

$$
L_n = H([L_0, L_1, L_2, \dots, L_{n-1}])
$$

Where $$H$$ is a composite function (typically batch normalization, ReLU, and convolution), and $$[L_0, L_1, \dots, L_{n-1}]$$ represents the concatenation of the feature maps from layers $$L_0$$ to $$L_{n-1}$$.

In contrast to architectures like ResNet, where each layer only connects to the next, DenseNet connects **every layer** to every subsequent layer within the same dense block.\
DenseNet 的核心组件是 **密集块**，其中所有层彼此连接。每个密集块由多个卷积层组成，每一层都将所有先前层的输出拼接作为输入。

例如，在一个有层 $$L_0, L_1, L_2, \dots, L_n$$ 的密集块中：

$$
L_n = H([L_0, L_1, L_2, \dots, L_{n-1}])
$$

其中，$$H$$ 是复合函数（通常是批归一化、ReLU 和卷积），$$[L_0, L_1, \dots, L_{n-1}]$$ 表示从层 $$L_0$$ 到 $$L_{n-1}$$ 的特征图拼接。

与 ResNet 等架构仅连接相邻层不同，DenseNet 在同一密集块内将**每一层**与所有后续层连接。

#### 3. **Growth Rate in DenseNet | DenseNet 的增长率**

**Growth rate** refers to the number of feature maps added by each layer in the dense block. For example, if the growth rate is 32, each layer will produce 32 feature maps, which are then concatenated with the feature maps from all previous layers. This ensures that the number of feature maps grows linearly with the number of layers in each block.\
**增长率** 指的是每个密集块中的每一层增加的特征图数量。例如，如果增长率为 32，每一层将生成 32 个特征图，并将这些特征图与所有先前层的特征图拼接。这确保了在每个块中，特征图的数量随着层数线性增长。

#### 4. **Transition Layers | 过渡层**

Between dense blocks, DenseNet uses **transition layers** to control the complexity of the model and reduce the size of feature maps. A transition layer typically consists of a batch normalization layer, a 1x1 convolution for reducing the number of feature maps, and a 2x2 average pooling layer to reduce the spatial dimensions of the feature maps.

Transition layers are important to prevent the network from becoming too large due to the concatenation of feature maps across many layers.\
在密集块之间，DenseNet 使用 **过渡层** 来控制模型的复杂性并减少特征图的大小。过渡层通常由批归一化层、用于减少特征图数量的 1x1 卷积层和用于减少特征图空间维度的 2x2 平均池化层组成。

过渡层对于防止网络因多个层的特征图拼接而变得过大至关重要。

#### 5. **DenseNet Variants | DenseNet 的变体**

DenseNet has several popular variants based on the number of layers:

* **DenseNet-121**: 121 layers deep, with 4 dense blocks.
* **DenseNet-169**: 169 layers deep, with 4 dense blocks.
* **DenseNet-201**: 201 layers deep, with 4 dense blocks.
* **DenseNet-264**: 264 layers deep, with 4 dense blocks.

Each variant differs in terms of the number of layers and the growth rate, but all follow the same basic structure of densely connected blocks followed by transition layers.\
DenseNet 有几个流行的变体，基于层数的不同：

* **DenseNet-121**：121 层深，具有 4 个密集块。
* **DenseNet-169**：169 层深，具有 4 个密集块。
* **DenseNet-201**：201 层深，具有 4 个密集块。
* **DenseNet-264**：264 层深，具有 4 个密集块。

每个变体在层数和增长率方面有所不同，但都遵循相同的基本结构，即密集连接块后接过渡层。

#### 6. **Why Use DenseNet? | 为什么使用 DenseNet？**

* **Efficient Feature Reuse | 高效的特征复用**: DenseNet promotes feature reuse by concatenating feature maps from previous layers, which leads to improved parameter efficiency and better performance. Each layer has access to all the features learned by the earlier layers, making the network more efficient in terms of both learning and computation. **高效的特征复用**：DenseNet 通过拼接先前层的特征图促进特征复用，从而提高了参数效率和性能。每一层都可以访问前面所有层学习到的特征，使得网络在学习和计算方面更加高效。
* **Improved Gradient Flow | 改善的梯度流动**: Because each layer has direct access to the gradients from the loss function, DenseNet mitigates the vanishing gradient problem. The connections between all layers help preserve the information flow during training. **改善的梯度流动**：由于每一层都可以直接访问来自损失函数的梯度，DenseNet 减轻了梯度消失问题。层与层之间的连接有助于在训练过程中保持信息流动。
* **Parameter Efficiency | 参数效率**: Despite being deep, DenseNet requires fewer parameters than architectures like ResNet. This is because feature maps are reused between layers, so the network does not need to generate as many new feature maps at each layer. **参数效率**：尽管网络很深，DenseNet 所需的参数比 ResNet 等架构少。这是因为特征图在层之间被复用，因此网络不需要在每一层生成太多新的特征图。

#### 7. **Limitations of DenseNet | DenseNet 的局限性**

* **High Memory Usage | 内存使用量大**: Because DenseNet concatenates feature maps from all previous layers, the model requires more memory than traditional architectures. This can become a bottleneck when training on high-resolution images or with very deep networks. **内存使用量大**：由于 DenseNet 将所有先前层的特征图拼接，模型的内存需求比传统架构更大。当训练高分辨率图像或非常深的网络时，这可能成为瓶颈。
* **Computation Overhead | 计算开销**: While DenseNet improves parameter efficiency, the need to concatenate feature maps at every layer can increase computational complexity, particularly for larger networks. **计算开销**：虽然 DenseNet 提高了参数效率，但在每一层拼接特征图的需求可能会增加计算复杂性，尤其对于较大的网络而言。

#### 8. **Example of DenseNet in Action | DenseNet 的操作示例**

Consider an example where DenseNet-121 is used to classify an image of a flower:

1. The image is passed through multiple **dense blocks**.
2. Each layer within the block receives the feature maps from all previous layers and concatenates them to generate richer representations.
3. **Transition layers** reduce the feature map size and complexity between dense blocks.
4. The output passes through a global average pooling layer and a softmax layer to predict the type of flower.

In this case, DenseNet efficiently reuses features from previous layers, leading to better feature extraction and improved classification accuracy.\
以 DenseNet-121 对花朵图像进行分类为例：

1. 图像通过多个 **密集块** 处理。
2. 块内的每一层接收来自所有先前层的特征图，并将它们拼接以生成更丰富的表示。
3. **过渡层** 在密集块之间减少特征图的大小和复杂性。
4. 输出通过全局平均池化层和 softmax 层预测花朵的种类。

在这种情况下，DenseNet 高效地复用了先前层的特征，从而实现了更好的特征提取和分类准确率的提高。



**DenseNet** 使用 **密集连接**，每一层的输入都来自所有先前层，从而促进特征复用并改善梯度流动。**密集块** 将先前层的特征图拼接在一起，使得学习更加高效，所需的参数也比传统架构少。优点包括高效的特征复用、改进的梯度流动和参数效率；缺点则是由于特征图拼接导致的高内存使用和计算开销较大。

## Extra Reading

* ResNet极大地改变了如何参数化深层网络中函数的观点。 _稠密连接网络_（DenseNet） ([Huang _et al._, 2017](https://zh.d2l.ai/chapter_references/zreferences.html#id73))在某种程度上是ResNet的逻辑扩展。让我们先从数学上了解一下。
* ResNet和DenseNet的关键区别在于，DenseNet输出&#x662F;_&#x8FDE;接_（用图中的$$[,]$$表示）而不是如ResNet的简单相加。 因此，在应用越来越复杂的函数序列后，我们执行从$$x$$到其展开式的映射
*   最后，将这些展开式结合到多层感知机中，再次减少特征的数量。 实现起来非常简单：我们不需要添加术语，而是将它们连接起来。 DenseNet这个名字由变量之间的“稠密连接”而得来，最后一层与之前的所有层紧密相连。

    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-05 at 3.52.54 PM.png" alt="" width="362"><figcaption></figcaption></figure>
* 稠密网络主要由2部分构成：_稠密块_（dense block）&#x548C;_&#x8FC7;渡层_（transition layer）。 前者定义如何连接输入和输出，而后者则控制通道数量，使其不会太复杂。

#### 稠密块体

* 一&#x4E2A;_&#x7A20;密&#x5757;_&#x7531;多个卷积块组成，每个卷积块使用相同数量的输出通道。 然而，在前向传播中，我们将每个卷积块的输入和输出在通道维上连结。

#### 过渡层

* 由于每个稠密块都会带来通道数的增加，使用过多则会过于复杂化模型。 而过渡层可以用来控制模型复杂度。 它通过$$1×1$$卷积层来减小通道数，并使用步幅为2的平均汇聚层减半高和宽，从而进一步降低模型复杂度。

#### DenseNet模型

* DenseNet首先使用同ResNet一样的单卷积层和最大汇聚层。
* 接下来，类似于ResNet使用的4个残差块，DenseNet使用的是4个稠密块。 与ResNet类似，我们可以设置每个稠密块使用多少个卷积层。 这里我们设成4，从而与 [7.6节](https://zh.d2l.ai/chapter_convolutional-modern/resnet.html#sec-resnet)的ResNet-18保持一致。 稠密块里的卷积层通道数（即增长率）设为32，所以每个稠密块将增加128个通道。
* 在每个模块之间，ResNet通过步幅为2的残差块减小高和宽，DenseNet则使用过渡层来减半高和宽，并减半通道数。
* 与ResNet类似，最后接上全局汇聚层和全连接层来输出结果。

