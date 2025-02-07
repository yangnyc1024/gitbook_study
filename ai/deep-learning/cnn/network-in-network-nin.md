# Network in Network(NiN)

## Network in Network (NiN) | 网络中的网络 (NiN)

#### 1. **What is Network in Network (NiN)? | 什么是网络中的网络 (NiN)？**

**Network in Network (NiN)** is a convolutional neural network architecture introduced by Min Lin, Qiang Chen, and Shuicheng Yan in their 2013 paper titled _"Network in Network."_ The key idea behind NiN is to enhance the representational power of CNNs by introducing a **"micro network"** to process local patches of an image. Instead of using a traditional convolutional layer followed by a linear transformation (like in VGG or AlexNet), NiN uses a small **multi-layer perceptron (MLP)** inside each receptive field.\
**网络中的网络 (NiN)** 是由 Min Lin、Qiang Chen 和 Shuicheng Yan 于 2013 年在他们的论文《网络中的网络》中提出的卷积神经网络架构。NiN 的核心思想是通过引入一个\*\*“微型网络”**来处理图像的局部区域，从而增强 CNN 的表示能力。与传统卷积层后接线性变换（如 VGG 或 AlexNet）不同，NiN 在每个感受野内使用一个小型的**多层感知器（MLP）\*\*。

#### 2. **How Does NiN Work? | NiN 是如何工作的？**

In traditional CNNs, a convolutional layer is followed by a non-linear activation function like ReLU. NiN replaces the convolutional layer's simple filter with an MLP that consists of multiple fully connected layers. These MLPs are applied to every receptive field, allowing for more complex and non-linear feature extraction at each local region.

* **Micro MLP Network | 微型 MLP 网络**: Instead of just convolving a single filter, NiN applies a small network of fully connected layers (usually 1x1 convolutions). These act as non-linear mappings that learn richer, more abstract features. **微型 MLP 网络**： NiN 不只是卷积单个滤波器，而是应用一个小型全连接层网络（通常是 1x1 卷积）。这些卷积作为非线性映射，可以学习更丰富、更抽象的特征。
* **1x1 Convolution | 1x1 卷积**: The key innovation in NiN is the use of **1x1 convolutions**, which function as MLPs for each pixel. These operations allow the network to combine channel-wise information while maintaining spatial dimensions. **1x1 卷积**： NiN 的关键创新是使用 **1x1 卷积**，它们在每个像素上充当 MLP。这些操作使网络能够在保持空间维度的同时组合通道维度的信息。
* **MLPConv Layer | MLPConv 层**: NiN replaces the standard convolution layer with an **MLPConv** layer, which is essentially a series of 1x1 convolutions that are followed by non-linear activation functions. This structure allows for a more complex non-linear feature extraction within local receptive fields. **MLPConv 层**： NiN 用 **MLPConv 层** 取代了标准卷积层，本质上是若干 1x1 卷积后接非线性激活函数的组合。这一结构允许在局部感受野内进行更复杂的非线性特征提取。

#### 3. **Architecture of NiN | NiN 的架构**

NiN follows a similar overall structure to traditional CNNs but replaces standard convolution layers with MLPConv layers. The general architecture includes:

* **MLPConv Layers**: These are convolutional layers with small filters (e.g., 1x1) followed by fully connected layers that act as local MLPs to extract more complex features.
* **Global Average Pooling | 全局平均池化**: Instead of using fully connected layers for classification, NiN uses global average pooling to compute the average of each feature map before classification. This reduces the risk of overfitting and lowers the number of parameters.
* **No Fully Connected Layers | 无全连接层**: NiN avoids traditional fully connected layers, which are common in architectures like AlexNet or VGG, making the network more parameter-efficient.

**Example NiN Architecture | NiN 架构示例**

1. **Input Layer | 输入层**: Input is a fixed-size image (e.g., 224x224 RGB image).
2. **MLPConv Layer 1 | MLPConv 层 1**: 96 5x5 filters followed by ReLU activation.
3. **Max Pooling Layer | 最大池化层**: A 2x2 max pooling layer to reduce spatial dimensions.
4. **MLPConv Layer 2 | MLPConv 层 2**: 256 5x5 filters followed by ReLU activation.
5. **Max Pooling Layer | 最大池化层**: Another 2x2 max pooling layer.
6. **MLPConv Layer 3 | MLPConv 层 3**: 384 3x3 filters.
7. **Global Average Pooling Layer | 全局平均池化层**: Replaces fully connected layers by averaging over feature maps.
8. **Softmax Output | Softmax 输出层**: Produces the final classification result.

#### 4. **Key Innovations of NiN | NiN 的关键创新**

* **1x1 Convolutions | 1x1 卷积**: NiN introduced the idea of using 1x1 convolutions to process each pixel individually while still capturing important information across channels. This was a major step forward in using CNNs to learn complex features. **1x1 卷积**：NiN 引入了使用 1x1 卷积的想法来单独处理每个像素，同时仍然捕捉跨通道的重要信息。这是 CNN 学习复杂特征的一个重大进步。
* **Global Average Pooling | 全局平均池化**: NiN replaced fully connected layers with global average pooling, which takes the average value of each feature map instead of flattening the feature maps into a vector. This reduced the number of parameters and helped prevent overfitting. **全局平均池化**：NiN 用全局平均池化替代了全连接层，池化是对每个特征图的平均值进行计算，而不是将特征图展平为向量。这减少了参数数量，有助于防止过拟合。
* **No Fully Connected Layers | 无全连接层**: NiN eliminates the need for fully connected layers, which makes the architecture more parameter-efficient and faster to compute. **无全连接层**：NiN 取消了全连接层的需求，使得架构在参数数量和计算效率方面表现更好。

#### 5. **Why Use NiN? | 为什么使用 NiN？**

* **Capturing Complex Features | 捕捉复杂特征**: By using MLPConv layers, NiN can capture more complex, non-linear patterns in the data than traditional CNNs. **捕捉复杂特征**：通过使用 MLPConv 层，NiN 能够比传统的 CNN 捕捉到数据中的更复杂的非线性模式。
* **Parameter Efficiency | 参数效率**: The 1x1 convolutions in NiN reduce the number of parameters while maintaining the network’s ability to learn rich features. **参数效率**：NiN 中的 1x1 卷积减少了参数数量，同时保持了网络学习丰富特征的能力。
* **Avoiding Overfitting | 避免过拟合**: Global average pooling reduces the risk of overfitting by not relying on large fully connected layers, making NiN more robust for tasks like image classification. **避免过拟合**：全局平均池化通过不依赖于大的全连接层，减少了过拟合的风险，使 NiN 在图像分类等任务中更加稳健。

#### 6. **Limitations of NiN | NiN 的局限性**

* **Training Complexity | 训练复杂性**: While NiN is effective at capturing complex patterns, training the micro-networks (MLPs) for each local region can be computationally expensive. **训练复杂性**：虽然 NiN 在捕捉复杂模式方面效果显著，但为每个局部区域训练微型网络（MLP）可能会增加计算成本。
* **Lack of Modularity | 缺乏模块化**: Unlike architectures like VGG, where convolutional blocks can be easily stacked, NiN’s reliance on MLPConv layers can make it harder to adapt or extend the architecture. **缺乏模块化**：与 VGG 等架构不同，VGG 的卷积块可以轻松堆叠，而 NiN 依赖于 MLPConv 层，这可能使得架构难以适应或扩展。

#### 7. **Example of NiN in Action | NiN 的操作示例**

Consider using NiN to classify an image of a car. The input image (224x224 RGB) is processed through the MLPConv layers:

* **First MLPConv Layer**: Detects basic edges and textures using 5x5 filters.
* **Second MLPConv Layer**: Extracts more detailed patterns like wheel shapes.
* **Third MLPConv Layer**: Captures the complex structure of the car body.

After passing through global average pooling, the network predicts that the image represents a car with a high confidence score.\
以 NiN 对汽车的图像进行分类为例。输入图像（224x224 RGB）通过 MLPConv 层处理：

* **第一个 MLPConv 层**：使用 5x5 卷积滤波器检测基本的边缘和纹理。
* **第二个 MLPConv 层**：提取更详细的模式，如车轮的形状。
* **第三个 MLPConv 层**：捕捉到汽车车身的复杂结构。

经过全局平均池化后，网络预测图像是汽车，并具有很高的置信度。



**NiN** 是一种 CNN 架构，通过 1x1 卷积作为小型多层感知器（MLP）来增强特征提取。它引入了 **MLPConv 层** 和 **全局平均池化**，取代了传统的全连接层。NiN 在捕捉复杂特征和防止过拟合方面具有优势，但由于计算复杂性较高，其模块化程度不如 VGG 等架构。

## Extra Reading

### NiN块

* 卷积层的输入和输出由四维张量组成，张量的每个轴分别对应样本、通道、高度和宽度。
* 另外，全连接层的输入和输出通常是分别对应于样本和特征的二维张量。 NiN的想法是在每个像素位置（针对每个高度和宽度）应用一个全连接层。
* 如果我们将权重连接到每个空间位置，我们可以将其视为$$1×1$$卷积层，或作为在每个像素位置上独立作用的全连接层。 从另一个角度看，即将空间维度中的每个像素视为单个样本，将通道维度视为不同特征（feature）。
* 下面的图说明了VGG和NiN及它们的块之间主要架构差异。 NiN块以一个普通卷积层开始，后面是两个$$1×1$$的卷积层。这两个$$1×1$$卷积层充当带有ReLU激活函数的逐像素全连接层。 第一层的卷积窗口形状通常由用户设置。 随后的卷积窗口形状固定为$$1×1$$。
*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-05 at 3.21.15 PM.png" alt=""><figcaption></figcaption></figure>



### NiN模型

* NiN使用窗口形状为$$11×11$$、$$5×5$$和$$3×3$$的卷积层，输出通道数量与AlexNet中的相同。 每个NiN块后有一个最大汇聚层，汇聚窗口形状为$$3×3$$，步幅为2。
* NiN和AlexNet之间的一个显著区别是NiN完全取消了全连接层。 相反，NiN使用一个NiN块，其输出通道数等于标签类别的数量。最后放一&#x4E2A;_&#x5168;局平均汇聚层_（global average pooling layer），生成一个对数几率 （logits）。
* NiN设计的一个优点是，它显著减少了模型所需参数的数量。然而，在实践中，这种设计有时会增加训练模型的时间。
* LeNet、AlexNet和VGG都有一个共同的设计模式：通过一系列的卷积层与汇聚层来提取空间结构特征；然后通过全连接层对特征的表征进行处理。 AlexNet和VGG对LeNet的改进主要在于如何扩大和加深这两个模块。
* 或者，可以想象在这个过程的早期使用全连接层。然而，如果使用了全连接层，可能会完全放弃表征的空间结构。 _网络中的网络_（_NiN_）提供了一个非常简单的解决方案：在每个像素的通道上分别使用多层感知机 ([Lin _et al._, 2013](https://zh.d2l.ai/chapter_references/zreferences.html#id93))

