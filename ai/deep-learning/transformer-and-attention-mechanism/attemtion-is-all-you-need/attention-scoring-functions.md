# Attention Scoring Functions

前文提到了使用了高斯核来对查询和键之间的关系建模。&#x20;

* 之前的高斯核指数部分可以视为注意力评分函数（attention scoring function），简称评分函数（scoring function），然后把这个函数的输出结果输入到softmax函数中进行归一化。
* 通过上述步骤，将得到与键对应的值的概率分布（即注意力权重）。
* 最后，注意力汇聚的输出就是基于这些注意力权重的值的加权和。

从宏观来看，上述算法可以用来实现基本的注意力机制框架。然而以下的图说明了如何将注意力汇聚的输出计算成为值的加权和，其中$$\alpha$$表示注意力评分函数。由于注意力权重是概率分布，因此加权和其本质上是加权平均值。

<figure><img src="../../../.gitbook/assets/Screenshot 2024-09-13 at 1.17.51 PM.png" alt="" width="375"><figcaption></figcaption></figure>

用数学语言描述，假设有一个查询$$q \in \mathbb{R}^{q}$$和$$m$$个“键-值”对$$(k_1, v_1), \dots, (k_m, v_m)$$，其中$$k_i \in \mathbb{R}^{k}, v_i \in \mathbb{R}^{v}$$。注意力汇聚函数$$f$$就被表示成值的加权和：

$$f(q, (k_1, v_1), \dots, (k_m, v_m)) = \sum_{i=1}^{m} \alpha(q, k_i)v_i \in \mathbb{R}^{v}$$

其中查询$$q$$和键$$k_i$$的注意力权重（标量）是通过注意力评分函数$$\alpha$$将两向量映射成标量，再经由softmax运算得到的：

$$\alpha(q, k_i) = \text{softmax}(\alpha(q, k_i)) = \frac{\exp(\alpha(q, k_i))}{\sum_{j=1}^{m} \exp(\alpha(q, k_j))} \in \mathbb{R}$$

选择不同的注意力评分函数$$\alpha$$会导致不同的注意力汇聚操作。

### 掩蔽softmax操作

* 据我们所知softmax的操作时用于输出一个概率分布作为注意力权重
* 在某些情况下，并非所有的值都应该被收纳道注意力汇聚中
* 比如说在一些高校处理小批量数据集的时候，某些文本序列被填充了没有意义的特殊词元
* 所以为了能将有意义的词元当作为值来获取注意力的汇聚，可以制定一个有效序列长度（即词元的个数），以便于在计算softmax时候过滤掉超出指定指定范围的位置。



## 加性注意力

一般来说，当查询和键是不同长度的矢量时，可以使用加性注意力作为评分函数。给定查询 $$q \in \mathbb{R}^{q}$$和 键 $$k \in \mathbb{R}^{k}$$，加性注意力（additive attention）的评分函数为：

$$a(q, k) = \mathbf{w_v}^\top \tanh(\mathbf{W_q}q + \mathbf{W_k}k) \in \mathbb{R}$$

其中可学习的参数是 $$\mathbf{W_q} \in \mathbb{R}^{h \times q}$$、$$\mathbf{W_k} \in \mathbb{R}^{h \times k}$$ 和 $$\mathbf{w_v} \in \mathbb{R}^{h}$$。将查询和键连接起来后输入到一个多层感知机（MLP）中，感知机包含一个隐藏层，其隐藏单元数是一个超参数 $$h$$。通过使用 $$\tanh$$ 作为激活函数，并且禁用偏置项。



## 缩放点积注意力

使用点积可以得到计算效率更高的评分函数，但是点积操作要求查询和键具有相同的长度 $$d$$。假设查询和键的所有元素都是独立的随机变量，并且都满足零均值和单位方差，那么两个向量的点积的均值为 0，方差为 $$d$$。为确保无论向量长度如何，点积的方差在不考虑向量长度的情况下仍然是常量，我们再将点积除以 $$\sqrt{d}$$，则缩放点积注意力（scaled dot-product attention）评分函数为：

$$a(q, k) = \frac{\mathbf{q}^\top \mathbf{k}}{\sqrt{d}}.$$

在实践中，我们通常从小批量的角度来考虑高效率，例如基于 $$n$$ 个查询和 $$m$$ 个键-值对计算注意力，其中查询和键的长度为 $$d$$，值的长度为 $$v_0$$。查询 $$\mathbf{Q} \in \mathbb{R}^{n \times d}$$，键 $$\mathbf{K} \in \mathbb{R}^{m \times d}$$ 和 值 $$\mathbf{V} \in \mathbb{R}^{m \times v}$$ 的缩放点积注意力是：$$\text{softmax} \left( \frac{\mathbf{Q}\mathbf{K}^\top}{\sqrt{d}} \right) \mathbf{V} \in \mathbb{R}^{n \times v}.$$
