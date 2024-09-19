# Padding& Stride

### Padding & Stride | 填充与步幅

#### 1. **Padding | 填充**

**What is Padding? | 什么是填充？**

Padding refers to the process of adding extra pixels (usually zeros) around the input image. This is done to control the spatial size of the output after a convolution operation and to preserve the edges of the image.\
填充指的是在输入图像周围添加额外的像素（通常是零）。这样做是为了在卷积操作后控制输出的空间大小，并且能够保留图像的边缘信息。

**Types of Padding | 填充类型**:

*   **Valid Padding (No Padding) | 有效填充（无填充）**: In this case, no padding is added to the image, and the output size shrinks after each convolution operation.\
    **公式**:

    $$
    \text{Output Size} = \frac{(\text{Input Size} - \text{Kernel Size})}{\text{Stride}} + 1
    $$
*   **Same Padding | 保持尺寸填充**: Padding is applied so that the output size remains the same as the input size. This is done by adding appropriate padding on all sides.\
    **公式**:

    $$
    \text{Output Size} = \frac{\text{Input Size}}{\text{Stride}}
    $$

**Example | 例子**:

* Input image size: $$4 \times 4$$
* Kernel size: $$3 \times 3$$
* Padding: $$1$$ (padding with one layer of zeros around the image)
* Output size (with stride 1): $$4 \times 4$$ (same as input size)

**Explanation | 解释**: Padding allows us to control the output size and helps retain more information near the borders of the image during convolution. Without padding, the output image will progressively shrink as we apply multiple convolution layers.

#### 2. **Stride | 步幅**

**What is Stride? | 什么是步幅？**

Stride refers to how many pixels the convolution filter moves at each step. The default stride is 1, meaning the filter moves one pixel at a time. A larger stride results in a smaller output size, as the filter skips pixels.\
步幅指的是卷积核每次移动时跨越的像素数量。默认的步幅是 1，意味着卷积核每次只移动一个像素。较大的步幅会导致输出尺寸变小，因为卷积核跳过了一些像素。

**Formula | 公式**: If the stride is $$S$$, the output size is calculated as:

$$
\text{Output Size} = \frac{(\text{Input Size} - \text{Kernel Size})}{S} + 1
$$

**Example | 例子**:

* Input image size: $$6 \times 6$$
* Kernel size: $$3 \times 3$$
* Stride: $$2$$
* No padding
*   **Output size**:

    $$
    \text{Output Size} = \frac{(6 - 3)}{2} + 1 = 2 + 1 = 3 \times 3
    $$

**Explanation | 解释**: A stride greater than 1 causes the filter to "skip" pixels, resulting in a smaller output. Stride controls the down-sampling of the image by reducing the spatial dimensions.

#### 3. **Padding and Stride Combined | 填充与步幅的结合**

Padding and stride often work together in convolutional layers to control the output dimensions. By adjusting both, we can tune the network to either preserve the input size (with appropriate padding and stride of 1) or reduce the input size (with larger strides and/or less padding).

**Example | 例子**:

* Input image size: $$5 \times 5$$
* Kernel size: $$3 \times 3$$
* Padding: $$1$$
* Stride: $$2$$
*   **Output size**:

    $$
    \text{Output Size} = \frac{(5 + 2 \times 1 - 3)}{2} + 1 = \frac{(5)}{2} + 1 = 3 \times 3
    $$

In this case, padding helps to preserve some of the image size, and stride reduces the spatial resolution of the output.

#### 4. **Why Use Padding and Stride? | 为什么使用填充和步幅？**

* **Why Use Padding? | 为什么使用填充？**
  * Padding allows you to preserve spatial dimensions, especially when you don't want your image to shrink after each convolution layer.
  * It is crucial for networks like Fully Convolutional Networks (FCNs) that need to retain the input resolution in tasks like segmentation.
  * 填充允许保留空间维度，尤其是在你不希望图像在每层卷积后缩小的情况下。
  * 在诸如全卷积网络（FCNs）等需要在分割任务中保留输入分辨率的网络中，填充非常重要。
* **Why Use Stride? | 为什么使用步幅？**
  * Stride helps reduce the computational complexity by downsampling the image.
  * It can be used as a form of dimensionality reduction without the need for pooling layers.
  * By using strides larger than 1, you can reduce the spatial dimensions more aggressively while preserving important features.
  * 步幅通过对图像进行下采样，有助于减少计算复杂度。
  * 它可以作为降维的一种形式，而无需使用池化层。
  * 通过使用大于 1 的步幅，可以更有效地减少空间维度，同时保留重要的特征。

#### 5. **When to Use Padding and Stride? | 什么时候使用填充和步幅？**

* **Padding** is typically used when you need to preserve the input size or when shrinking the image would result in losing important features. It is widely used in image segmentation tasks and when the spatial structure is important.\
  **填充** 通常用于需要保留输入尺寸或图像缩小会导致丢失重要特征时。它广泛用于图像分割任务以及空间结构重要的情况。
* **Stride** is useful when you want to downsample the image to reduce its size and computational load, especially in tasks like image classification. By using stride, you can achieve a smaller output size with fewer layers.\
  **步幅** 在你希望对图像进行下采样以减小尺寸和计算负荷时非常有用，尤其是在图像分类任务中。通过使用步幅，你可以通过较少的层次实现较小的输出尺寸。

#### Summary | 总结

* **Padding** allows for control over the output size and helps retain edge information in the image.\
  **填充**可以控制输出的大小，并帮助保留图像中的边缘信息。
* **Stride** controls how much the filter moves during the convolution. Larger strides lead to smaller outputs.\
  **步幅**控制卷积核在操作过程中移动的距离。较大的步幅会导致较小的输出。

Combining padding and stride allows us to design convolutional layers with precise control over the output dimensions, which is crucial for deep learning models.\
通过结合填充与步幅，我们可以精确地控制卷积层的输出尺寸，这在深度学习模型中至关重要。
