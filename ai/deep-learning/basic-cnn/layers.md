# Layers

## Convolution Layer in CNN | 卷积神经网络中的卷积层

#### 1. **What is a Convolution Layer? | 什么是卷积层？**

A **Convolution Layer** is the core building block of a Convolutional Neural Network (CNN). It is designed to automatically and adaptively learn spatial hierarchies of features in input data such as images. The convolution operation applies a filter (or kernel) over the input data to produce a feature map, highlighting certain aspects of the input like edges, textures, and more.\
**卷积层** 是卷积神经网络（CNN）的核心组成部分。它的设计目的是自动且自适应地学习输入数据（如图像）中的空间特征层次。卷积操作通过在输入数据上应用滤波器（或称为卷积核）来生成特征图，突出输入的某些方面，如边缘、纹理等。

#### 2. **How Does a Convolution Layer Work? | 卷积层是如何工作的？**

The convolution layer works by sliding a filter over the input data. At each step (defined by the **stride**), the filter performs element-wise multiplication with a portion of the input and sums the results to produce a single output value in the feature map.\
卷积层通过在输入数据上滑动卷积核来工作。每一步（由**步幅**定义），卷积核会与输入数据的一部分进行逐元素相乘，并将结果相加生成特征图中的一个输出值。

For example, given an input image $$I$$ and a filter (kernel) $$K$$, the output of the convolution at a location $$(i,j)$$ is computed as:

$$
O(i, j) = \sum_m \sum_n I(i+m, j+n) \cdot K(m,n)
$$

where $$m$$ and $$n$$ are the dimensions of the filter.\
例如，给定一个输入图像 $$I$$ 和一个滤波器（卷积核） $$K$$，在位置 $$(i, j)$$ 处的卷积输出计算如下：

$$
O(i, j) = \sum_m \sum_n I(i+m, j+n) \cdot K(m,n)
$$

其中 $$m$$ 和 $$n$$ 是卷积核的维度。

#### 3. **Components of a Convolution Layer | 卷积层的组成部分**

* **Filters (Kernels) | 滤波器（卷积核）**: These are the small matrices (e.g., 3x3 or 5x5) used to scan over the input. Different filters capture different features such as edges or textures.\
  **滤波器（卷积核）**：这些是用于扫描输入数据的小矩阵（例如 3x3 或 5x5）。不同的滤波器捕捉不同的特征，如边缘或纹理。
* **Stride | 步幅**: Stride controls how much the filter moves over the input. A larger stride reduces the output size by skipping pixels.\
  **步幅**：步幅控制卷积核在输入数据上移动的步数。较大的步幅通过跳过像素来减少输出尺寸。
* **Padding | 填充**: Padding adds extra pixels around the input to control the output size, often used to maintain the spatial dimensions.\
  **填充**：填充是在输入数据的周围添加额外的像素，以控制输出尺寸，通常用于保持空间维度不变。
* **Activation Function | 激活函数**: After convolution, an activation function like ReLU (Rectified Linear Unit) is applied to introduce non-linearity into the model.\
  **激活函数**：卷积操作后，会应用如 ReLU（修正线性单元）等激活函数，以引入非线性。

#### 4. **Why Use Convolution Layers? | 为什么使用卷积层？**

* **Local Feature Detection | 局部特征检测**: Convolution layers are excellent at detecting local features in the data, such as edges, corners, and textures.\
  **局部特征检测**：卷积层非常擅长检测数据中的局部特征，如边缘、角点和纹理。
* **Parameter Efficiency | 参数效率**: Instead of learning separate weights for every pixel like in fully connected layers, convolution layers use shared weights (filters), which reduces the number of parameters drastically.\
  **参数效率**：卷积层通过共享权重（滤波器），而不是为每个像素学习单独的权重，从而大幅减少参数数量。
* **Translation Invariance | 平移不变性**: Convolution layers can recognize features (e.g., edges) regardless of their location in the input, providing translation invariance.\
  **平移不变性**：卷积层能够识别特征（例如边缘），无论它们在输入中的位置如何，从而提供了平移不变性。

#### 5. **Example: How a Convolution Layer Works | 例子：卷积层如何工作**

Let’s consider a simple 5x5 input image and a 3x3 filter. The filter slides over the input image, performing element-wise multiplication at each step and summing the results to create the output feature map.

Given the input:

$$
\text{Input} = \begin{bmatrix} 1 & 1 & 1 & 0 & 0 \\ 0 & 1 & 1 & 1 & 0 \\ 0 & 0 & 1 & 1 & 1 \\ 1 & 1 & 0 & 0 & 0 \\ 0 & 1 & 1 & 0 & 0 \end{bmatrix}
$$

And the filter (kernel):

$$
\text{Kernel} = \begin{bmatrix} 1 & 0 & -1 \\ 1 & 0 & -1 \\ 1 & 0 & -1 \end{bmatrix}
$$

The output after applying the convolution will be:

$$
\text{Output} = \begin{bmatrix} 2 & 1 & -1 \\ 1 & 2 & 0 \\ 1 & 2 & 1 \end{bmatrix}
$$

This process highlights how the convolution layer extracts specific features from the input image, such as vertical edges in this case.\
假设我们有一个简单的 5x5 输入图像和一个 3x3 滤波器。卷积核在输入图像上滑动，每一步进行逐元素相乘，并将结果相加生成输出特征图。

输入为：

$$
\text{输入} = \begin{bmatrix} 1 & 1 & 1 & 0 & 0 \\ 0 & 1 & 1 & 1 & 0 \\ 0 & 0 & 1 & 1 & 1 \\ 1 & 1 & 0 & 0 & 0 \\ 0 & 1 & 1 & 0 & 0 \end{bmatrix}
$$

滤波器（卷积核）为：

$$
\text{卷积核} = \begin{bmatrix} 1 & 0 & -1 \\ 1 & 0 & -1 \\ 1 & 0 & -1 \end{bmatrix}
$$

应用卷积后的输出为：

$$
\text{输出} = \begin{bmatrix} 2 & 1 & -1 \\ 1 & 2 & 0 \\ 1 & 2 & 1 \end{bmatrix}
$$

这个过程展示了卷积层如何从输入图像中提取特定特征，例如在此例中检测到的垂直边缘。

#### 6. **When to Use Convolution Layers? | 什么时候使用卷积层？**

* **Image Processing | 图像处理**: Convolution layers are most commonly used in image-related tasks like classification, detection, and segmentation.\
  **图像处理**：卷积层最常用于图像相关的任务，如分类、检测和分割。
* **Feature Extraction | 特征提取**: Convolution layers are excellent for extracting hierarchical features, from low-level edges to high-level object parts.\
  **特征提取**：卷积层非常适合从低级边缘到高级物体部分提取层次化特征。
* **Handling Structured Data | 处理结构化数据**: Beyond images, convolution layers can be used for structured data like audio signals, time series, or even text.\
  **处理结构化数据**：除了图像，卷积层还可以用于处理音频信号、时间序列甚至文本等结构化数据。

## Pooling Layer in CNN | 卷积神经网络中的池化层



#### 1. **What is a Pooling Layer? | 什么是池化层？**

A **Pooling Layer** is another fundamental component in Convolutional Neural Networks (CNNs). The primary purpose of pooling is to downsample the input, reducing its spatial dimensions while retaining important features. This helps to make the model more efficient and less prone to overfitting.\
**池化层** 是卷积神经网络（CNN）中的另一个重要组成部分。池化的主要目的是对输入进行下采样，减少其空间维度，同时保留重要特征。这有助于提高模型的效率并减少过拟合的可能性。

#### 2. **How Does a Pooling Layer Work? | 池化层是如何工作的？**

Pooling layers work by sliding a window (usually 2x2 or 3x3) over the input, and at each step, they perform a downsampling operation. The two most common pooling operations are **max pooling** and **average pooling**:

* **Max Pooling | 最大池化**: The window selects the maximum value from the region of the input covered by the window. $$\text{Max Pooling Output} = \max(x_1, x_2, x_3, x_4)$$ **最大池化**：池化窗口从覆盖的区域中选择最大值。
* **Average Pooling | 平均池化**: The window calculates the average of the values from the region of the input covered by the window. $$\text{Average Pooling Output} = \frac{1}{n} \sum_{i=1}^n x_i$$ **平均池化**：池化窗口计算覆盖区域的平均值。

For example, for a 2x2 max pooling operation, given the following input:

$$
\text{Input} = \begin{bmatrix} 1 & 3 & 2 & 4 \\ 5 & 6 & 7 & 8 \\ 3 & 2 & 1 & 0 \\ 9 & 8 & 5 & 6 \end{bmatrix}
$$

After applying 2x2 max pooling, the output would be:

$$
\text{Max Pooling Output} = \begin{bmatrix} 6 & 8 \\ 9 & 6 \end{bmatrix}
$$

#### 3. **Why Use Pooling Layers? | 为什么使用池化层？**

* **Dimensionality Reduction | 降维**: Pooling reduces the size of the input, making the model more computationally efficient by reducing the number of parameters and computations required in the subsequent layers.\
  **降维**：池化减少输入的大小，使模型在后续层中更高效地计算，减少了所需的参数和计算量。
* **Prevent Overfitting | 防止过拟合**: By reducing the dimensionality, pooling layers help avoid overfitting, as the model focuses on the most significant features, rather than memorizing fine details.\
  **防止过拟合**：通过降维，池化层帮助模型避免过拟合，因为模型将专注于最重要的特征，而不是记住细节。
* **Translation Invariance | 平移不变性**: Pooling introduces a degree of translation invariance. This means the model becomes less sensitive to small shifts or distortions in the input, improving its robustness.\
  **平移不变性**：池化引入了一定程度的平移不变性，这意味着模型对输入中的小偏移或失真不太敏感，从而提高了其鲁棒性。

#### 4. **Types of Pooling Layers | 池化层的类型**

* **Max Pooling | 最大池化**: Commonly used in CNNs because it extracts the most prominent features from the input, making it more efficient at capturing sharp features like edges.\
  **最大池化**：在 CNN 中常用，因为它提取输入中的最突出的特征，使其更有效地捕捉到像边缘这样的显著特征。
* **Average Pooling | 平均池化**: It is often used when smoothing the input is desired, such as in cases where more general or averaged features are important.\
  **平均池化**：通常用于需要对输入进行平滑处理的情况下，例如在一些更广泛的或平均特征较重要的任务中。
* **Global Pooling | 全局池化**: This operation applies pooling across the entire input, resulting in a single value for each feature map. It is often used in the final layers of a network before classification.\
  **全局池化**：这种操作在整个输入上应用池化，导致每个特征图得到一个单一的值。它通常用于分类之前网络的最后几层。

#### 5. **Example of Pooling Operation | 池化操作的例子**

Consider a simple 4x4 input matrix and apply 2x2 max pooling:

**Input:**

$$
\text{Input} = \begin{bmatrix} 1 & 3 & 2 & 4 \\ 5 & 6 & 7 & 8 \\ 3 & 2 & 1 & 0 \\ 9 & 8 & 5 & 6 \end{bmatrix}
$$

**Max Pooling (2x2):**

* For the first 2x2 region: $$\max(1, 3, 5, 6) = 6$$
* For the second 2x2 region: $$\max(2, 4, 7, 8) = 8$$
* For the third 2x2 region: $$\max(3, 2, 9, 8) = 9$$
* For the fourth 2x2 region: $$\max(1, 0, 5, 6) = 6$$

**Output:**

$$
\text{Max Pooling Output} = \begin{bmatrix} 6 & 8 \\ 9 & 6 \end{bmatrix}
$$

In this case, max pooling selects the highest value from each 2x2 window, reducing the spatial dimensions of the input matrix from 4x4 to 2x2.\
在这个例子中，最大池化从每个 2x2 窗口中选择最大值，将输入矩阵的空间维度从 4x4 缩小到 2x2。

#### 6. **When to Use Pooling Layers? | 什么时候使用池化层？**

* **After Convolution Layers | 卷积层之后**: Pooling layers are commonly used after convolution layers to reduce the size of feature maps and make the model more efficient.\
  **卷积层之后**：池化层通常用于卷积层之后，减少特征图的大小，使模型更高效。
* **For Dimensionality Reduction | 降低维度**: When the model's input becomes too large, pooling can be used to downsample the data, making the network less computationally expensive.\
  **用于降维**：当模型的输入变得过大时，可以使用池化来对数据进行下采样，从而降低网络的计算开销。
* **In Tasks Requiring Robustness | 需要鲁棒性的任务**: Pooling layers are particularly useful in tasks where small shifts or distortions in the input (e.g., in image classification) should not affect the overall output of the model.\
  **在需要鲁棒性的任务中**：在一些任务中，输入中的小偏移或失真（例如图像分类）不应影响模型的整体输出，此时池化层特别有用。

## Fully-connected Layer in Neural Networks | 神经网络中的全连接层

#### 1. **What is a Fully-connected Layer? | 什么是全连接层？**

A **Fully-connected Layer** (also known as a dense layer) is a layer in which every neuron (node) is connected to every neuron in the previous layer and the next layer. It is a traditional layer used in feedforward neural networks. Each connection has a corresponding weight, and the neuron computes a weighted sum of the inputs, adds a bias term, and then applies an activation function to produce the output.\
**全连接层**（也称为密集层）是神经网络中的一种层，层中的每个神经元都与前一层和下一层中的每个神经元相连接。它是前馈神经网络中使用的传统层。每个连接都有一个对应的权重，神经元计算输入的加权和，再加上一个偏置项，然后应用激活函数来产生输出。

#### 2. **How Does a Fully-connected Layer Work? | 全连接层是如何工作的？**

In a fully-connected layer, each neuron performs the following operations:

* **Weighted Sum | 加权和**: For each neuron, the inputs are multiplied by their corresponding weights and summed: $$z = w_1x_1 + w_2x_2 + \dots + w_nx_n + b$$ where:
  * $$w_1, w_2, \dots, w_n$$ are the weights,
  * $$x_1, x_2, \dots, x_n$$ are the inputs,
  * $$b$$ is the bias term.
* **Activation Function | 激活函数**: After computing the weighted sum, an activation function (such as ReLU, Sigmoid, or Tanh) is applied to introduce non-linearity: $$y = f(z)$$ where $$f$$ is the activation function.\
  在全连接层中，每个神经元执行以下操作：
  * **加权和**：每个神经元将输入与对应的权重相乘并求和： $$z = w_1x_1 + w_2x_2 + \dots + w_nx_n + b$$ 其中：
    * $$w_1, w_2, \dots, w_n$$ 是权重，
    * $$x_1, x_2, \dots, x_n$$ 是输入，
    * $$b$$ 是偏置项。
  * **激活函数**：在计算加权和之后，应用激活函数（如 ReLU、Sigmoid 或 Tanh）引入非线性： $$y = f(z)$$\
    其中 $$f$$ 是激活函数。

#### 3. **Why Use Fully-connected Layers? | 为什么使用全连接层？**

* **Feature Combination | 特征组合**: Fully-connected layers combine the features learned by previous layers (e.g., convolutional layers) and use them to make predictions.\
  **特征组合**：全连接层将前面层（如卷积层）学习到的特征进行组合，并利用这些特征进行预测。
* **Global Information | 全局信息处理**: Unlike convolutional layers, which process local features, fully-connected layers capture global patterns from the entire input. This is crucial for tasks like classification, where the overall structure of the input matters.\
  **全局信息处理**：与卷积层处理局部特征不同，全连接层从整个输入中捕捉全局模式。这在分类等任务中至关重要，因为输入的整体结构很重要。
* **Non-linearity | 非线性**: By applying activation functions, fully-connected layers introduce non-linearity, enabling the network to learn complex relationships between inputs and outputs.\
  **非线性**：通过应用激活函数，全连接层引入了非线性，使网络能够学习输入和输出之间的复杂关系。

#### 4. **Example of a Fully-connected Layer | 全连接层的例子**

Consider a fully-connected layer with 3 input neurons and 2 output neurons. The input is represented as a vector $$X = [x_1, x_2, x_3]$$, and the weights and biases are represented as:

$$
W = \begin{bmatrix} w_{11} & w_{12} & w_{13} \\ w_{21} & w_{22} & w_{23} \end{bmatrix}, \quad B = \begin{bmatrix} b_1 \\ b_2 \end{bmatrix}
$$

The output of this layer is calculated as:

$$
Z = W \cdot X + B = \begin{bmatrix} w_{11} & w_{12} & w_{13} \\ w_{21} & w_{22} & w_{23} \end{bmatrix} \cdot \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} + \begin{bmatrix} b_1 \\ b_2 \end{bmatrix}
$$

Each neuron in the output computes a weighted sum of the inputs and applies the activation function:

$$
y_1 = f(w_{11}x_1 + w_{12}x_2 + w_{13}x_3 + b_1)
$$

$$
y_2 = f(w_{21}x_1 + w_{22}x_2 + w_{23}x_3 + b_2)
$$

This process generates two output values from the three input values.\
假设一个全连接层有 3 个输入神经元和 2 个输出神经元。输入表示为向量 $$X = [x_1, x_2, x_3]$$，权重和偏置表示为：

$$
W = \begin{bmatrix} w_{11} & w_{12} & w_{13} \\ w_{21} & w_{22} & w_{23} \end{bmatrix}, \quad B = \begin{bmatrix} b_1 \\ b_2 \end{bmatrix}
$$

该层的输出计算为：

$$
Z = W \cdot X + B = \begin{bmatrix} w_{11} & w_{12} & w_{13} \\ w_{21} & w_{22} & w_{23} \end{bmatrix} \cdot \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} + \begin{bmatrix} b_1 \\ b_2 \end{bmatrix}
$$

输出中的每个神经元计算输入的加权和并应用激活函数：

$$
y_1 = f(w_{11}x_1 + w_{12}x_2 + w_{13}x_3 + b_1)
$$

$$
y_2 = f(w_{21}x_1 + w_{22}x_2 + w_{23}x_3 + b_2)
$$

这个过程将 3 个输入值生成 2 个输出值。

#### 5. **When to Use Fully-connected Layers? | 什么时候使用全连接层？**

* **At the End of CNNs | 在 CNN 的末端**: In Convolutional Neural Networks, fully-connected layers are typically used at the end of the network to aggregate the features extracted by convolutional and pooling layers and make final predictions (e.g., classification).\
  **在 CNN 的末端**：在卷积神经网络中，全连接层通常用于网络的末端，汇总卷积层和池化层提取的特征并进行最终预测（如分类）。
* **For Classification Tasks | 用于分类任务**: Fully-connected layers are most commonly used in classification tasks, where the network needs to map learned features to specific categories or labels.\
  **用于分类任务**：全连接层最常用于分类任务中，网络需要将学习到的特征映射到特定类别或标签上。
* **For Regression Tasks | 用于回归任务**: Fully-connected layers can also be used in regression tasks to output continuous values, such as predicting prices, sales, or time series values.\
  **用于回归任务**：全连接层还可以用于回归任务中，输出连续值，如预测价格、销量或时间序列值。

#### 6. **Limitations of Fully-connected Layers | 全连接层的局限性**

* **Large Number of Parameters | 参数数量庞大**: Fully-connected layers can have a large number of parameters, especially when used with high-dimensional inputs (e.g., images). This increases the risk of overfitting and makes the model computationally expensive.\
  **参数数量庞大**：全连接层的参数数量较多，特别是在处理高维输入（如图像）时。这增加了过拟合的风险，并使模型计算复杂度增加。
* **Not Efficient for Spatial Data | 对空间数据处理效率不高**: For tasks like image processing, fully-connected layers do not preserve the spatial structure of the input, making them less efficient than convolutional layers for such tasks.\
  **对空间数据处理效率不高**：对于图像处理等任务，全连接层不能保留输入的空间结构，因此在此类任务中效率不如卷积层。



## Non-linearity and ReLU Layer in Neural Networks | 神经网络中的非线性层和 ReLU 层

#### 1. **What is Non-linearity in Neural Networks? | 什么是神经网络中的非线性？**

In neural networks, **non-linearity** refers to the introduction of a non-linear function into the model. Without non-linearity, the neural network would behave like a simple linear model, regardless of the number of layers. Non-linear activation functions allow the network to model complex relationships between inputs and outputs by adding non-linear transformations after each layer.\
在神经网络中，**非线性** 是指在模型中引入非线性函数。如果没有非线性，无论有多少层，神经网络都会像一个简单的线性模型一样工作。通过在每一层后添加非线性转换，非线性激活函数使网络能够建模输入和输出之间的复杂关系。

#### 2. **Why Non-linearity is Important? | 为什么非线性很重要？**

* **Modeling Complex Data | 建模复杂数据**: Non-linearity enables the network to capture more complex patterns in the data. Linear layers alone cannot solve problems that require non-linear decision boundaries, like recognizing images, language processing, etc.\
  **建模复杂数据**：非线性使网络能够捕捉数据中的更复杂模式。仅依赖线性层无法解决需要非线性决策边界的问题，比如图像识别、语言处理等。
* **Stacking Layers | 堆叠多层**: Non-linear activation functions allow for multiple layers in a neural network to be stacked. Without non-linearity, stacking layers would not add more expressiveness to the model.\
  **堆叠多层**：非线性激活函数使得神经网络可以堆叠多层。如果没有非线性，堆叠层数并不会增加模型的表达能力。

#### 3. **What is the ReLU Layer? | 什么是 ReLU 层？**

**ReLU (Rectified Linear Unit)** is one of the most commonly used non-linear activation functions in neural networks. It is simple and efficient, defined as:

$$
f(x) = \max(0, x)
$$

This means that for any input $$x$$, if $$x$$ is positive, the output is $$x$$; otherwise, the output is zero.\
**ReLU（修正线性单元）** 是神经网络中最常用的非线性激活函数之一。它简单且高效，定义为：

$$
f(x) = \max(0, x)
$$

这意味着对于任何输入 $$x$$，如果 $$x$$ 为正，则输出为 $$x$$；否则，输出为零。

#### 4. **Why Use ReLU? | 为什么使用 ReLU？**

* **Efficient and Simple | 高效且简单**: ReLU is computationally efficient because it involves only a simple thresholding operation. Compared to other activation functions (like Sigmoid or Tanh), ReLU is faster to compute.\
  **高效且简单**：ReLU 计算非常高效，因为它只涉及简单的阈值操作。与其他激活函数（如 Sigmoid 或 Tanh）相比，ReLU 计算速度更快。
* **Avoids Vanishing Gradient Problem | 避免梯度消失问题**: Unlike Sigmoid or Tanh, which can lead to very small gradients during backpropagation, ReLU avoids the vanishing gradient problem for positive values. This allows gradients to flow more effectively during training.\
  **避免梯度消失问题**：与 Sigmoid 或 Tanh 不同，ReLU 避免了反向传播中梯度变得非常小的问题（梯度消失）。这使得梯度在训练过程中能够更有效地传播。
* **Sparse Activation | 稀疏激活**: In ReLU, neurons are activated only if the input is positive. This leads to sparse activation, meaning that fewer neurons are activated at the same time, which makes the model more efficient and faster to compute.\
  **稀疏激活**：在 ReLU 中，只有当输入为正时，神经元才会被激活。这导致稀疏激活，即同一时间内较少的神经元被激活，这使得模型更高效，计算速度更快。

#### 5. **Limitations of ReLU | ReLU 的局限性**

* **Dying ReLU Problem | ReLU 死亡问题**: When the input to a ReLU neuron is always negative, the gradient becomes zero, and the neuron stops learning. This is known as the "dying ReLU" problem, where certain neurons can permanently die during training.\
  **ReLU 死亡问题**：当 ReLU 神经元的输入始终为负时，梯度变为零，神经元停止学习。这就是所谓的“ReLU 死亡问题”，即在训练过程中某些神经元会永久失效。
* **Unbounded Output | 无界输出**: ReLU's output for positive values can be very large, potentially leading to exploding gradients in some scenarios.\
  **无界输出**：对于正值，ReLU 的输出可以非常大，这在某些情况下可能导致梯度爆炸问题。

#### 6. **Other Non-linear Activation Functions | 其他非线性激活函数**

*   **Sigmoid | Sigmoid 函数**: The sigmoid function is another activation function defined as: $$f(x) = \frac{1}{1 + e^{-x}}$$ It maps the input into a range between 0 and 1, but can suffer from vanishing gradients.

    **Sigmoid 函数**：Sigmoid 是另一种激活函数，定义为： $$f(x) = \frac{1}{1 + e^{-x}}$$ 它将输入映射到 0 到 1 之间的范围，但容易出现梯度消失问题。
*   **Tanh | 双曲正切函数**: The Tanh activation function is defined as: $$f(x) = \tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}$$ It maps the input to a range between -1 and 1 and can also face vanishing gradients.

    **双曲正切函数**：Tanh 激活函数定义为： $$f(x) = \tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}$$ 它将输入映射到 -1 到 1 之间的范围，也会面临梯度消失的问题。
*   **Leaky ReLU | 带泄漏的 ReLU**: To address the "dying ReLU" problem, Leaky ReLU allows a small, non-zero gradient for negative inputs: $$f(x) = \max(0.01x, x)$$

    **带泄漏的 ReLU**：为了解决“ReLU 死亡问题”，Leaky ReLU 对负输入引入了一个小的非零梯度： $$f(x) = \max(0.01x, x)$$

#### 7. **Example of ReLU Operation | ReLU 操作的例子**

Suppose we have an input vector:

$$
X = \begin{bmatrix} -2 & 3 & -1 & 5 \end{bmatrix}
$$

After applying the ReLU activation function:

$$
f(X) = \begin{bmatrix} 0 & 3 & 0 & 5 \end{bmatrix}
$$

In this example, negative values are replaced with 0, and positive values remain unchanged.\
假设我们有一个输入向量：

$$
X = \begin{bmatrix} -2 & 3 & -1 & 5 \end{bmatrix}
$$

应用 ReLU 激活函数后：

$$
f(X) = \begin{bmatrix} 0 & 3 & 0 & 5 \end{bmatrix}
$$

在这个例子中，负值被替换为 0，而正值保持不变。

#### 8. **When to Use ReLU? | 什么时候使用 ReLU？**

* **In Hidden Layers | 隐藏层中使用**: ReLU is commonly used in the hidden layers of deep neural networks because of its simplicity and efficiency.\
  **隐藏层中使用**：ReLU 常用于深度神经网络的隐藏层，因为它简单且高效。
* **For Large-scale Models | 用于大规模模型**: ReLU is often used in large models with many layers, where avoiding the vanishing gradient problem is crucial for effective training.\
  **用于大规模模型**：ReLU 常用于层数较多的大规模模型中，避免梯度消失问题对于有效训练非常重要。

## Batch Normalization



