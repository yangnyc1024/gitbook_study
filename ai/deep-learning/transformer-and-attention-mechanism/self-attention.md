# Self-Attention

### Self-Attention

* 由于查询、键和值来自同一组输入，因此被称为 自注意力（self-attention） (Lin et al., 2017, Vaswani et al., 2017)， 也被称为内部注意力（intra-attention） (Cheng et al., 2016, Parikh et al., 2016, Paulus et al., 2017)。
* 给定一个由词元组成的输入序列$$x_1,\cdots, x_n$$， 其中任意$$x_i \in \mathbb{R}^d$$（$$1\leq i \leq n$$）。 该序列的自注意力输出为一个长度相同的序列 $$y_1,\cdots, y_n$$，其中：

$$y_i = f(x_i, (x_1, x_1), \cdot,(x_n, x_n)) \in \mathbb{R}^d$$，

### Comparing CNNs, RNNs, and Self-Attention



<figure><img src="../../.gitbook/assets/Screenshot 2024-02-29 at 1.15.51 PM.png" alt="" width="375"><figcaption></figcaption></figure>

* 考虑一个卷积核大小为$$k$$的卷积层。 在后面的章节将提供关于使用卷积神经网络处理序列的更多详细信息。
* 目前只需要知道的是，由于序列长度是$$n$$，输入和输出的通道数量都是$$d$$， 所以卷积层的计算复杂度为$$O(knd^2)$$。因此卷积神经网络是分层的，因此为有$$O(1)$$个顺序操作， 最大路径长度为$$O(n/k)$$。 例如，图中卷积核大小为3的双层卷积神经网络的感受野内。
* 当更新循环神经网络的隐状态时， $$d \times d$$权重矩阵和$$d$$维隐状态的乘法计算复杂度为$$O(d^2)$$。 由于序列长度为$$n$$，因此循环神经网络层的计算复杂度为$$O(nd^2)$$。 根据图， 有$$O(n)$$个顺序操作无法并行化，最大路径长度也是$$O(n)$$。

### Positional Encoding

* 在处理词元序列时，循环神经网络是逐个的重复地处理词元的， 而自注意力则因为并行计算而放弃了顺序操作。 为了使用序列的顺序信息，通过在输入表示中添加 _位置编码_（positional encoding）来注入绝对的或相对的位置信息。&#x20;
* 绝对位置信息
* 相对位置信息



