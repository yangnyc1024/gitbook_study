# Why CNN

## 为什么选择卷积神经网络（CNN）？ | Why Choose Convolutional Neural Networks (CNN)?

#### 1. **捕捉空间特征 | Captures Spatial Features**

CNN 擅长处理图像数据，因为它可以捕捉到数据中的空间结构。通过卷积操作，CNN 可以识别图像中的边缘、纹理和形状等局部特征。\
CNN excels at handling image data because it captures spatial structures in the data. Through convolution, CNN can identify local features such as edges, textures, and shapes.

#### 2. **参数更少 | Fewer Parameters**

相比全连接网络，CNN 使用共享权重的卷积核，大大减少了需要学习的参数。这让网络更加高效，降低了过拟合的风险。\
Compared to fully connected networks, CNN uses shared weights in convolutional filters, significantly reducing the number of parameters to learn. This makes the network more efficient and reduces the risk of overfitting.

#### 3. **平移不变性 | Translation Invariance**

卷积操作使得 CNN 对图像中的平移变得不敏感。无论一个物体出现在图像的哪个位置，CNN 都可以识别出来。\
The convolution operation allows CNNs to be invariant to translations in the image. CNN can recognize objects regardless of where they appear in the image.

#### 4. **自动特征提取 | Automatic Feature Extraction**

CNN 的多层结构可以自动从低级特征（如边缘）到高级特征（如物体）进行提取，无需人工设计特征。\
The multi-layer structure of CNNs allows them to automatically extract features from low-level (e.g., edges) to high-level (e.g., objects), eliminating the need for manual feature design.

#### 5. **池化层降低维度 | Dimensionality Reduction via Pooling**

池化操作（如最大池化）可以有效地减少数据维度，同时保留关键特征，降低计算成本，并增加对噪声的鲁棒性。\
Pooling operations (e.g., max pooling) efficiently reduce data dimensions while preserving key features, lowering computational cost, and making the network more robust to noise.

#### 6. **处理高维数据 | Handles High-Dimensional Data**

对于图像这样的高维数据（例如 224x224 的 RGB 图像有超过 150,000 个输入值），CNN 能通过局部连接和池化操作更好地处理这些复杂的输入。\
For high-dimensional data like images (e.g., a 224x224 RGB image has over 150,000 input values), CNNs handle this complexity more effectively through local connections and pooling.

## Convolution and Filter in Image Processing

*   图像处理中的卷积操作就是利用卷积核（卷积模板/滤波矩阵/kernel/filter）在图片上滑动，将图像点上的像素灰度值与对应的卷积核上的数值相乘，然后将所有相乘后的值相加作为卷积核中间像素对应的图像上像素的灰度值，并最终滑动完成所有图像的过程。


* 对图像和卷积核进行逐个元素相乘再求和的操作就相当于将一个二维的函数移动到另一个二维函数的所有位置，这个操作就叫卷积（convolution）或者互相关（cross-correlation）。卷积和相关的差别是，在数学上，卷积需要先对卷积核进行水平和垂直方向的翻转，然后再对前面的矩阵像素相乘求和的操作。但如果矩阵是对称的，那么两者就没有什么差别了。深度学习中的卷积操作在数学上准确度来说称为互相关。
