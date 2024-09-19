# Networks Using Blocks (VGG)

### Networks Using Blocks: VGG | 使用模块化结构的网络：VGG

#### 1. **What is VGG? | 什么是 VGG？**

**VGG** is a convolutional neural network (CNN) architecture proposed by the Visual Geometry Group (VGG) from Oxford University, primarily developed by Karen Simonyan and Andrew Zisserman. VGG was introduced in the 2014 paper titled _"Very Deep Convolutional Networks for Large-Scale Image Recognition"_ and became well-known for its simplicity and performance on the ImageNet dataset. VGG-16 and VGG-19 are the most popular variants.\
**VGG** 是由牛津大学视觉几何组（VGG）提出的一种卷积神经网络（CNN）架构，主要由 Karen Simonyan 和 Andrew Zisserman 开发。VGG 在 2014 年的论文《非常深的卷积网络用于大规模图像识别》中被提出，以其简洁的设计和在 ImageNet 数据集上的出色表现而闻名。最流行的变体是 VGG-16 和 VGG-19。

#### 2. **Architecture of VGG | VGG 的架构**

The key idea behind VGG is the use of **small, fixed-size convolution filters (3x3)** and stacking them to build deep networks. VGG uses **blocks of convolutional layers** followed by pooling layers to progressively reduce the spatial dimensions of the feature maps. Below is an overview of VGG's architecture:

* **Input Layer | 输入层**: The input to VGG is a fixed-size 224x224 RGB image. The image is first passed through a stack of convolutional layers. 输入 VGG 的是固定大小的 224x224 的 RGB 图像。图像首先经过一堆卷积层。
* **Convolutional Blocks | 卷积模块**: Instead of using large filters, VGG uses multiple 3x3 convolution filters in each block. This approach helps capture more complex patterns while keeping the number of parameters manageable.
  * A typical block has 2 or 3 convolutional layers, each followed by a ReLU activation function.
  * VGG 不使用大卷积核，而是在每个模块中使用多个 3x3 的卷积核。这种方法可以捕捉到更多复杂的模式，同时保持参数数量可控。
  * 一个典型的卷积模块有 2 或 3 层卷积层，每层后面跟着 ReLU 激活函数。
* **Max Pooling Layers | 最大池化层**: After each convolutional block, a max pooling layer (2x2) is applied to reduce the spatial dimensions of the feature maps.
  * Pooling helps reduce computation and prevents overfitting.
  * 在每个卷积模块之后，会应用一个 2x2 的最大池化层来减少特征图的空间维度。
  * 池化有助于减少计算量并防止过拟合。
* **Fully Connected Layers | 全连接层**: After the convolutional blocks and pooling layers, the output is flattened and passed through 3 fully connected layers with 4096, 4096, and 1000 neurons respectively. 在卷积模块和池化层之后，输出被展平并通过 3 个全连接层，分别具有 4096、4096 和 1000 个神经元。
* **Output Layer | 输出层**: The final fully connected layer has 1000 neurons, which corresponds to the 1000 classes in the ImageNet dataset. A softmax function is applied to produce the final classification probabilities. 最后的全连接层有 1000 个神经元，分别对应于 ImageNet 数据集中的 1000 个类别。应用 softmax 函数来产生最终的分类概率。

#### 3. **VGG-16 and VGG-19 | VGG-16 和 VGG-19**

VGG has two popular variants:

* **VGG-16**: 13 convolutional layers + 3 fully connected layers = 16 layers.
* **VGG-19**: 16 convolutional layers + 3 fully connected layers = 19 layers.

Both networks use the same building blocks (3x3 convolution and 2x2 max pooling), but VGG-19 is deeper, making it capable of capturing more complex features at the cost of higher computational requirements.\
VGG 有两个流行的变体：

* **VGG-16**：13 层卷积层 + 3 层全连接层 = 16 层。
* **VGG-19**：16 层卷积层 + 3 层全连接层 = 19 层。

两个网络都使用相同的构建块（3x3 卷积和 2x2 最大池化），但 VGG-19 更深，能够捕捉更复杂的特征，代价是更高的计算要求。

#### 4. **Why Use VGG? | 为什么使用 VGG？**

* **Simplicity and Modularity | 简单性和模块化**: VGG's architecture is straightforward, based on stacking small 3x3 convolution filters. This modular design is simple yet powerful, making it easy to understand and implement. **简单性和模块化**：VGG 的架构非常直观，基于堆叠小的 3x3 卷积核。这种模块化设计既简单又强大，易于理解和实现。
* **Deeper Networks | 更深的网络**: By using smaller filters and stacking them, VGG demonstrated that deeper networks can perform better on complex tasks like image recognition. **更深的网络**：通过使用更小的卷积核并堆叠，VGG 证明了更深的网络在图像识别等复杂任务中可以表现得更好。
* **Parameter Efficiency | 参数效率**: VGG replaces large filters (like 5x5 or 7x7) with multiple 3x3 filters, reducing the number of parameters while maintaining the same receptive field size. **参数效率**：VGG 使用多个 3x3 卷积核替换大卷积核（如 5x5 或 7x7），在保持相同感受野的情况下减少了参数数量。
* **Transfer Learning | 迁移学习**: VGG models are commonly used for **transfer learning**. Pre-trained VGG models on ImageNet are often fine-tuned for other tasks like object detection or segmentation due to their strong feature extraction capabilities. **迁移学习**：VGG 模型通常用于 **迁移学习**。在 ImageNet 上预训练的 VGG 模型经常被微调用于其他任务，如目标检测或图像分割，因为它们具有很强的特征提取能力。

#### 5. **Limitations of VGG | VGG 的局限性**

* **Large Model Size | 模型尺寸大**: VGG models, especially VGG-19, have a very large number of parameters (e.g., VGG-16 has over 138 million parameters). This makes them computationally expensive to train and deploy. **模型尺寸大**：VGG 模型，特别是 VGG-19，具有非常多的参数（例如，VGG-16 有超过 1.38 亿个参数）。这使得它们的训练和部署计算成本较高。
* **Slow to Train | 训练速度慢**: Due to its depth and large number of parameters, VGG takes a long time to train on large datasets, even with modern GPUs. **训练速度慢**：由于其深度和大量参数，即使在现代 GPU 上，VGG 在大规模数据集上的训练也需要较长时间。
* **No Batch Normalization | 缺少批归一化**: VGG does not include **batch normalization**, which has become a standard technique in later architectures (like ResNet) to improve training stability and speed. **缺少批归一化**：VGG 没有包含 **批归一化**，而批归一化已经成为后续架构（如 ResNet）中的标准技术，用于提高训练的稳定性和速度。

#### 6. **Example of VGG in Action | VGG 的操作示例**

Consider an example where VGG-16 is used to classify an image of a cat. The input image (224x224 RGB) is processed through the convolutional blocks:

* **First block**: Detects simple features like edges.
* **Second and third blocks**: Extracts more detailed textures and patterns.
* **Fourth and fifth blocks**: Captures complex shapes and structures.

Finally, the output of the convolutional blocks is passed through the fully connected layers, which classify the image into one of 1000 categories (e.g., “tabby cat”).\
以 VGG-16 对猫的图像进行分类为例。输入图像（224x224 RGB）通过卷积模块处理：

* **第一个模块**：检测简单的特征，如边缘。
* **第二和第三模块**：提取更详细的纹理和模式。
* **第四和第五模块**：捕捉复杂的形状和结构。

最后，卷积模块的输出通过全连接层，将图像分类为 1000 个类别之一（例如，“虎斑猫”）。









## 使用块的网络

* 与芯片设计中工程师从放置晶体管到逻辑元件再到逻辑块的过程类似，神经网络架构的设计也逐渐变得更加抽象。研究人员开始从单个神经元的角度思考问题，发展到整个层，现在又转向块，重复层的模式。
* 使用块的想法首先出现在牛津大学的视觉几何组（visual geometry group）的VGG网络中。通过使用循环和子程序，可以很容易地在任何现代深度学习框架的代码中实现这些重复的架构。



## VGG块

* review经典卷积神经网络的基本组成部分是下面的这个序列：
  * 带填充以保持分辨率的卷积层；
  * 非线性激活函数，如ReLU；
  * 汇聚层，如最大汇聚层。
* 一个VGG块与之类似，由一系列卷积层组成，后面再加上用于空间下采样的最大汇聚层。
* 在最初的VGG论文中 ([Simonyan and Zisserman, 2014](https://zh.d2l.ai/chapter\_references/zreferences.html#id153))，作者使用了带有$$3×3$$卷积核、填充为1（保持高度和宽度）的卷积层，和带有$$2×2$$汇聚窗口、步幅为2（每个块后的分辨率减半）的最大汇聚层。

## VGG网络

* 其中有超参数变量`conv_arch`。该变量指定了每个VGG块里卷积层个数和输出通道数。全连接模块则与AlexNet中的相同。
* 原始VGG网络有5个卷积块，其中前两个块各有一个卷积层，后三个块各包含两个卷积层。 第一个模块有64个输出通道，每个后续模块将输出通道数量翻倍，直到该数字达到512。由于该网络使用8个卷积层和3个全连接层，因此它通常被称为VGG-11。

<figure><img src="../../../.gitbook/assets/Screenshot 2024-02-05 at 10.51.00 AM.png" alt=""><figcaption></figcaption></figure>



* 与芯片设计中工程师从放置晶体管到逻辑元件再到逻辑块的过程类似，神经网络架构的设计也逐渐变得更加抽象。研究人员开始从单个神经元的角度思考问题，发展到整个层，现在又转向块，重复层的模式。
* 使用块的想法首先出现在牛津大学的[视觉几何组（visual geometry group）](http://www.robots.ox.ac.uk/\~vgg/)的_VGG网络_中。通过使用循环和子程序，可以很容易地在任何现代深度学习框架的代码中实现这些重复的架构。
