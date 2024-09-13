# Multi-Head Attention

在实践中

* 当给定相同的查询，键和值的集合时，我们希望模型可以基于相同的注意力机制学习到不同的行为，然后将不同的行为作为知识组合起来，捕获序列内各种范围的依赖关系（短距离依赖和长距离依赖关系）
* 因此，允许注意力机制组合使用查询，键和值的不同子空间表示（representation subspaces）可能是有益的

所以

* 与其单独使用a single attention pooling,queries, keys,，我们可以用独立学习得到的$$h$$ 组不同的线性投影(linear prjections)来变化查询，键和值。
* 然后这$$h$$ 组变换后的查询，键和值将并行地送到注意力汇聚中。
* 最后，将这$$h$$ 个主利益汇聚的输出拼接在一起，并且通过另一个可以学习的线性投影进行变换，以产生最终输出

这就是multihead attention多头注意力。

* 在其中，对于$$h$$ 个注意力汇聚输出，每一个注意力汇聚都被称为一个头（head）
* 如图所示
*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-14 at 3.12.12 PM.png" alt="" width="375"><figcaption></figcaption></figure>





## Model

* 在实现多头注意力之前，让我们用数学语言将这个模型形式化地描述出来。给定查询向量 $$\mathbf{q} \in \mathbb{R}^{d_q}$$、键向量 $$\mathbf{k} \in \mathbb{R}^{d_k}$$ 和值向量 $$\mathbf{v} \in \mathbb{R}^{d_v}$$，每个注意力头 $$\mathbf{h}_i \ (i = 1, \dots, h)$$ 的计算方法为：

&#x20;                                                $$\mathbf{h}_i = f(\mathbf{W}_i^{(q)} \mathbf{q}, \mathbf{W}_i^{(k)} \mathbf{k}, \mathbf{W}_i^{(v)} \mathbf{v}) \in \mathbb{R}^{p_v},$$

* 其中，可学习的参数包括 $$\mathbf{W}_i^{(q)} \in \mathbb{R}^{p_q \times d_q}$$、$$\mathbf{W}_i^{(k)} \in \mathbb{R}^{p_k \times d_k}$$ 和 $$\mathbf{W}_i^{(v)} \in \mathbb{R}^{p_v \times d_v}$$，以及代表注意力汇聚的函数 $$f$$。$$f$$ 可以是 **加性注意力** 和 **缩放点积注意力**。
* 多头注意力的输出需要经过另一个线性转换，它对应着 $$h$$ 个头连接后的结果，因此其可学习参数是 $$\mathbf{W}_o \in \mathbb{R}^{p_o \times h p_v}$$：

$$\mathbf{W}_o \begin{bmatrix} \mathbf{h}_1 \ \vdots \ \mathbf{h}_h \end{bmatrix} \in \mathbb{R}^{p_o}.$$\
