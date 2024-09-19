# Residual Networks(ResNet) and ResNeXt

## Residual Networks (ResNet) and ResNeXt | 残差网络（ResNet）和 ResNeXt

#### 1. **What is ResNet? | 什么是 ResNet？**

**ResNet (Residual Networks)** is a deep convolutional neural network (CNN) architecture introduced by Kaiming He and his colleagues in their 2015 paper _"Deep Residual Learning for Image Recognition."_ ResNet was revolutionary because it allowed the training of **very deep networks** by addressing the **vanishing gradient problem** through **residual connections**. ResNet models won the ImageNet Large Scale Visual Recognition Challenge (ILSVRC) in 2015 with impressive performance.\
**ResNet（残差网络）** 是由 Kaiming He 和他的团队在 2015 年的论文《用于图像识别的深度残差学习》中提出的卷积神经网络（CNN）架构。ResNet 革命性地解决了深层网络中的 **梯度消失问题**，通过引入 **残差连接**，使得 **非常深的网络** 能够成功训练。ResNet 在 2015 年的 ImageNet 大规模视觉识别挑战赛（ILSVRC）中表现出色并获得冠军。

#### 2. **Residual Connections | 残差连接**

The key innovation of ResNet is the **residual connection** (or **skip connection**). Instead of learning the direct mapping of the input to the output, ResNet learns the **residual** (or difference) between the input and the output. This is done by adding the input directly to the output of a few convolutional layers. The residual block is expressed as:

$$
y = F(x) + x
$$

Where:

* $$x$$ is the input,
* $$F(x)$$ represents the output of the convolutional layers (or residual function),
* $$y$$ is the final output.

This structure allows gradients to flow more easily through deeper networks, preventing the **vanishing gradient problem** that often arises in very deep networks.\
ResNet 的核心创新是 **残差连接**（或称为 **跳跃连接**）。ResNet 不直接学习输入到输出的映射，而是学习输入与输出之间的 **残差**（即差异）。这是通过将输入直接添加到几层卷积层的输出中实现的。残差块的表达式为：

$$
y = F(x) + x
$$

其中：

* $$x$$ 是输入，
* $$F(x)$$ 代表卷积层的输出（或称为残差函数），
* $$y$$ 是最终输出。

这种结构使得梯度可以更容易地通过更深的网络流动，从而避免在非常深的网络中常见的 **梯度消失问题**。

#### 3. **Architecture of ResNet | ResNet 的架构**

ResNet is built using **residual blocks** that contain skip connections. The most common variants of ResNet include:

* **ResNet-18**: 18 layers deep, using 8 residual blocks.
* **ResNet-34**: 34 layers deep, using 16 residual blocks.
* **ResNet-50**: 50 layers deep, using 16 residual blocks but with **bottleneck layers** (3 layers per block instead of 2).
* **ResNet-101**: 101 layers deep, using 33 residual blocks.
* **ResNet-152**: 152 layers deep, using 50 residual blocks.

**Example of Residual Block | 残差块示例**

In a typical ResNet block:

1. The input passes through two or three convolutional layers with batch normalization and ReLU activation.
2. A skip connection adds the input directly to the output of the block.
3. The result is then passed to the next block.

Example residual block for ResNet-34:

$$
y = F(x) + x
$$

Where $$F(x)$$ is a 2-layer convolution, followed by batch normalization and ReLU activation.\
在典型的 ResNet 残差块中：

1. 输入通过两个或三个卷积层，伴随批归一化和 ReLU 激活。
2. 跳跃连接将输入直接添加到块的输出中。
3. 结果传递到下一个残差块。

ResNet-34 的残差块示例：

$$
y = F(x) + x
$$

其中 $$F(x)$$ 是一个两层卷积，后接批归一化和 ReLU 激活。

#### 4. **Why Use ResNet? | 为什么使用 ResNet？**

* **Training Very Deep Networks | 训练非常深的网络**: ResNet allows the training of networks with hundreds or even thousands of layers without suffering from the vanishing gradient problem. **训练非常深的网络**：ResNet 允许训练具有数百甚至数千层的网络，而不会遇到梯度消失问题。
* **Residual Learning | 残差学习**: By learning the residual (the difference between input and output), ResNet makes it easier to optimize deep networks and ensures faster convergence. **残差学习**：通过学习残差（输入与输出之间的差异），ResNet 使得优化深层网络更加容易，并确保更快的收敛速度。
* **Performance in Image Classification | 图像分类的表现**: ResNet achieved state-of-the-art performance on ImageNet and was a significant step forward in deep learning. **图像分类的表现**：ResNet 在 ImageNet 上取得了领先的表现，是深度学习领域的重要进展。

#### 5. **ResNeXt: Extension of ResNet | ResNeXt：ResNet 的扩展**

**ResNeXt** is an improved variant of ResNet, introduced in 2017 by Saining Xie and others in the paper _"Aggregated Residual Transformations for Deep Neural Networks."_ ResNeXt builds on the idea of **ResNet** by introducing a concept called **cardinality**, which refers to the number of parallel branches within a residual block.\
**ResNeXt** 是 ResNet 的改进变体，由 Saining Xie 等人在 2017 年的论文《用于深度神经网络的聚合残差变换》中提出。ResNeXt 基于 **ResNet** 的思想，提出了一个称为 **基数（cardinality）** 的概念，即残差块中并行分支的数量。

#### 6. **How ResNeXt Works? | ResNeXt 是如何工作的？**

In ResNeXt, instead of just increasing the depth or width of the network, the architecture adds **more parallel paths** inside each residual block. This creates a **multi-branch structure** similar to GoogLeNet's Inception modules, but the branches are identical and follow a simple pattern of 1x1, 3x3, and 1x1 convolutions. Each branch processes different subsets of features in parallel, and their outputs are aggregated before passing to the next block.

* **Cardinality**: This refers to the number of parallel branches in the network. Increasing cardinality improves the model's capacity to learn more complex representations.
* **Grouped Convolutions**: ResNeXt uses **grouped convolutions** in which convolution filters are split into groups, allowing for more efficient computation.\
  在 ResNeXt 中，网络不只是增加深度或宽度，而是在每个残差块中增加了 **更多的并行路径**。这创建了一个与 GoogLeNet 的 Inception 模块类似的**多分支结构**，但这些分支是相同的，并遵循简单的 1x1、3x3 和 1x1 卷积模式。每个分支并行处理不同的特征子集，它们的输出在传递到下一个残差块之前被聚合。
* **基数（Cardinality）**：这是指网络中并行分支的数量。增加基数可以提高模型学习更复杂表示的能力。
* **分组卷积**：ResNeXt 使用 **分组卷积**，即将卷积滤波器分成组，允许更高效的计算。

#### 7. **Why Use ResNeXt? | 为什么使用 ResNeXt？**

* **Better Scalability | 更好的可扩展性**: ResNeXt scales better than ResNet as it allows for increasing the number of parallel branches (cardinality) without greatly increasing computational cost. **更好的可扩展性**：ResNeXt 比 ResNet 更具可扩展性，因为它允许增加并行分支（基数）而不会大幅增加计算成本。
* **Performance Improvement | 性能提升**: ResNeXt achieves higher accuracy on various image classification benchmarks than ResNet with fewer layers, thanks to its increased capacity for learning complex features. **性能提升**：ResNeXt 在许多图像分类基准测试中，比 ResNet 以更少的层数实现了更高的准确率，这归功于其对复杂特征学习能力的提升。

#### 8. **Comparison: ResNet vs. ResNeXt | 比较：ResNet 与 ResNeXt**

\| **Aspect | 方面** | **ResNet** | **ResNeXt** | |------------------------|------------------------------------------|--------------------------------------------| | Residual Blocks | Basic skip connections with 2 or 3 layers. | Uses multiple parallel branches inside each block. | | Depth vs. Cardinality | Increases depth (more layers). | Increases cardinality (more parallel branches). | | Convolutions | Standard convolutions. | Grouped convolutions to reduce computation. | | Performance | Strong performance on deep networks. | Better scalability and efficiency with high cardinality. |

#### 9. **Example of ResNeXt Block | ResNeXt 模块示例**

In a ResNeXt block:

* **Input**: An input feature map.
* **Multiple parallel paths**: Each path applies a series of convolutions (e.g., 1x1, 3x3, 1x1).
* **Aggregation**: The outputs from each parallel path are concatenated and summed before passing to the next block.

This structure enhances the model’s capacity to capture diverse features without a significant increase in computational cost.\
在 ResNeXt 模块中：

* **输入**：一个输入特征图。
* **多个并行路径**：每个路径应用一系列卷积（如 1x1、3x3、1x1）。
* **聚合**：每个并行路径的输出被拼接并求和，然后传递到下一个块。

这种结构增强了模型捕捉多样化特征的能力，而不会显著增加计算成本。





**ResNet** 使用残差连接解决梯度消失问题，允许训练非常深的网络（如 ResNet-50、ResNet-101）。**ResNeXt** 基于 ResNet 通过增加每个残差块中的 **基数（cardinality）** 来提高特征提取能力，而不会显著增加复杂性。ResNet 的优点是深度网络没有梯度消失问题，在图像识别中表现出色；ResNeXt 的优点是可扩展性好、计算效率高，并且通过增加基数提高了准确率。

## Extra Reading

* 只有当较复杂的函数类包含较小的函数类时，我们才能确保提高它们的性能。 对于深度神经网络，如果我们能将新添加的层训练成_恒等映射_（identity function）$$f(x) = x$$，新模型和原模型将同样有效。 同时，由于新模型可能得出更优的解来拟合训练数据集，因此添加层似乎更容易降低训练误差。
* 针对这一问题，何恺明等人提出了_残差网络_（ResNet） ([He _et al._, 2016](https://zh.d2l.ai/chapter\_references/zreferences.html#id60))。 它在2015年的ImageNet图像识别挑战赛夺魁，并深刻影响了后来的深度神经网络的设计。
* &#x20;残差网络的核心思想是：每个附加层都应该更容易地包含原始函数作为其元素之一。 于是，_残差块_（residual blocks）便诞生了，这个设计对如何建立深层神经网络产生了深远的影响。 凭借它，ResNet赢得了2015年ImageNet大规模视觉识别挑战赛。

#### Residual Block

* 让我们聚焦于神经网络局部：如图所示，假设我们的原始输入为$$x$$，而希望学出的理想映射为$$f(x)$$
* 左图虚线框中的部分需要直接拟合出该映射$$f(x)$$，而右图虚线框中的部分则需要拟合出残差映射$$f(x) - x$$。 残差映射在现实中往往更容易优化。
* &#x20;以本节开头提到的恒等映射作为我们希望学出的理想映射$$f(x)$$，我们只需将图中右图虚线框内上方的加权运算（如仿射）的权重和偏置参数设成0，那么$$f(x)$$即为恒等映射。
* &#x20;实际中，当理想映射$$f(x)$$极接近于恒等映射时，残差映射也易于捕捉恒等映射的细微波动。 右图是ResNet的基础架构–_残差块_（residual block）。 在残差块中，输入可通过跨层数据线路更快地向前传播。
*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-05 at 3.43.41 PM.png" alt="" width="375"><figcaption></figcaption></figure>
* ResNet沿用了VGG完整的$$3×3$$卷积层设计。 残差块里首先有2个有相同输出通道数的$$3×3$$卷积层。 每个卷积层后接一个批量规范化层和ReLU激活函数。 然后我们通过跨层数据通路，跳过这2个卷积运算，将输入直接加在最后的ReLU激活函数前。

#### ResNet模型

* ResNet的前两层跟之前介绍的GoogLeNet中的一样： 在输出通道数为64、步幅为2的$$7×7$$卷积层后，接步幅为2的$$3×3$$的最大汇聚层。 不同之处在于ResNet每个卷积层后增加了批量规范化层。
* GoogLeNet在后面接了4个由Inception块组成的模块。 ResNet则使用4个由残差块组成的模块，每个模块使用若干个同样输出通道数的残差块。 第一个模块的通道数同输入通道数一致。 由于之前已经使用了步幅为2的最大汇聚层，所以无须减小高和宽。 之后的每个模块在第一个残差块里将上一个模块的通道数翻倍，并将高和宽减半。

#### Summary

* 学习嵌套函数（nested function）是训练神经网络的理想情况。在深层神经网络中，学习另一层作为恒等映射（identity function）较容易（尽管这是一个极端情况）。
* 残差映射可以更容易地学习同一函数，例如将权重层中的参数近似为零。
* 利用残差块（residual blocks）可以训练出一个有效的深层神经网络：输入可以通过层间的残余连接更快地向前传播。
* 残差网络（ResNet）对随后的深层神经网络设计产生了深远影响。
