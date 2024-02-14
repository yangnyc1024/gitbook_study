# Multi-Head Attention

* Instead of performing a single attention pooling, queries, keys, and values can be transformed with $$ℎ$$ independently learned linear projections.&#x20;
* Then these $$ℎ$$ projected queries, keys, and values are fed into attention pooling in parallel. In the end, $$ℎ$$ attention-pooling outputs are concatenated and transformed with another learned linear projection to produce the final output.&#x20;
* This design is called _multi-head attention_, where each of the $$ℎ$$ attention pooling outputs is a _head_ ([Vaswani _et al._, 2017](https://d2l.ai/chapter\_references/zreferences.html#id302)).&#x20;
* Using fully connected layers to perform learnable linear transformations, the following figure describes multi-head attention.
*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-14 at 3.12.12 PM.png" alt="" width="375"><figcaption></figcaption></figure>
* 为此，与其只使用单独一个注意力汇聚， 我们可以用独立学习得到的$$ℎ$$组不同的 _线性投影_（linear projections）来变换查询、键和值。 然后，这$$ℎ$$组变换后的查询、键和值将并行地送到注意力汇聚中。&#x20;
* 最后，将这$$ℎ$$个注意力汇聚的输出拼接在一起， 并且通过另一个可以学习的线性投影进行变换， 以产生最终输出。 这种设计被称为_多头注意力_（multihead attention） ([Vaswani _et al._, 2017](https://zh.d2l.ai/chapter\_references/zreferences.html#id174))。 对于$$ℎ$$个注意力汇聚输出，每一个注意力汇聚都被称作一个_头_（head）。



#### Model

* 在实现多头注意力之前，让我们用数学语言将这个模型形式化地描述出来。 给定查询$$q\in \mathbb{R^{d_q}}$$、 键$$k \in \mathbb{R}^{d_k}$$和 值$$v \in \mathbb{R}^{d_v}$$， 每个注意力头$$h_i$$（$$(i = 1, \cdots, h)$$）的计算方法为：

$$h_i = f(W_i^{(q)}, W_i^{(k)}, W_{i}^{(v)}v) \in \mathbb{R}^{p_v}$$

* 其中，可学习的参数包括 $$W_i^{(q)} \in \mathbb{R}^{p_q \times d_q}$$、 $$W_i^{(k)} \in \mathbb{R}^{p_k  \times d_k}$$和 $$W_i^{(v)} \in \mathbb{R}^{p_v \times d_v}$$， 以及代表注意力汇聚的函数$$f$$。
* &#x20;$$f$$可以是加性注意力和缩放点积注意力。&#x20;
*   多头注意力的输出需要经过另一个线性转换， 它对应着$$ℎ$$个头连结后的结果，因此其可学习参数是  $$W_0 \in \mathbb{R}^{p_0 \times hp_v}$$, 基于这种设计，每个头都可能会关注输入的不同部分， 可以表示比简单加权平均值更复杂的函数。

    \
