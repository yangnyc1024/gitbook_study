# Densely Coneected Networks(DenseNet)

* ResNet极大地改变了如何参数化深层网络中函数的观点。 _稠密连接网络_（DenseNet） ([Huang _et al._, 2017](https://zh.d2l.ai/chapter\_references/zreferences.html#id73))在某种程度上是ResNet的逻辑扩展。让我们先从数学上了解一下。
* ResNet和DenseNet的关键区别在于，DenseNet输出是_连接_（用图中的$$[,]$$表示）而不是如ResNet的简单相加。 因此，在应用越来越复杂的函数序列后，我们执行从$$x$$到其展开式的映射
*   最后，将这些展开式结合到多层感知机中，再次减少特征的数量。 实现起来非常简单：我们不需要添加术语，而是将它们连接起来。 DenseNet这个名字由变量之间的“稠密连接”而得来，最后一层与之前的所有层紧密相连。

    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-05 at 3.52.54 PM.png" alt="" width="362"><figcaption></figcaption></figure>
* 稠密网络主要由2部分构成：_稠密块_（dense block）和_过渡层_（transition layer）。 前者定义如何连接输入和输出，而后者则控制通道数量，使其不会太复杂。

#### 稠密块体

* 一个_稠密块_由多个卷积块组成，每个卷积块使用相同数量的输出通道。 然而，在前向传播中，我们将每个卷积块的输入和输出在通道维上连结。

#### 过渡层

* 由于每个稠密块都会带来通道数的增加，使用过多则会过于复杂化模型。 而过渡层可以用来控制模型复杂度。 它通过$$1×1$$卷积层来减小通道数，并使用步幅为2的平均汇聚层减半高和宽，从而进一步降低模型复杂度。

#### DenseNet模型

* DenseNet首先使用同ResNet一样的单卷积层和最大汇聚层。
* 接下来，类似于ResNet使用的4个残差块，DenseNet使用的是4个稠密块。 与ResNet类似，我们可以设置每个稠密块使用多少个卷积层。 这里我们设成4，从而与 [7.6节](https://zh.d2l.ai/chapter\_convolutional-modern/resnet.html#sec-resnet)的ResNet-18保持一致。 稠密块里的卷积层通道数（即增长率）设为32，所以每个稠密块将增加128个通道。
* 在每个模块之间，ResNet通过步幅为2的残差块减小高和宽，DenseNet则使用过渡层来减半高和宽，并减半通道数。
* 与ResNet类似，最后接上全局汇聚层和全连接层来输出结果。

