# Attention Mechanism

## Attention Mechanism (注意力机制)

The attention mechanism helps address problems found in the RNN-based encoder-decoder setup. As illustrated in Fig. 2.2, an attention mechanism is like a memory bank. When queried, it produces an output based on stored keys and values (Bahdanau et al., 2014).

注意力机制有助于解决 RNN 结构中编码器-解码器的相关问题。如图 2.2 所示，注意力机制类似于一个记忆库。当查询时，它根据存储的键（keys）和值（values）生成输出（Bahdanau et al., 2014）。

### Attention Formulation (注意力机制公式)

Let us consider the memory unit consisting of $$n$$ key-value pairs $$(\mathbf{k}_1, \mathbf{v}_1), \dots, (\mathbf{k}_n, \mathbf{v}_n)$$ with $$\mathbf{k}_i \in \mathbb{R}^{d_k}$$ and $$\mathbf{v}_i \in \mathbb{R}^{d_v}$$ . The attention layer receives an input as query $$\mathbf{q} \in \mathbb{R}^{d_q}$$ and returns an output $$\mathbf{o} \in \mathbb{R}^{d_v}$$ with the same shape as the value $$\mathbf{v}$$ .

我们考虑一个存储单元，由 $$n$$ 组键值对 $$(\mathbf{k}_1, \mathbf{v}_1), \dots, (\mathbf{k}_n, \mathbf{v}_n)$$ 组成，其中 $$\mathbf{k}_i \in \mathbb{R}^{d_k}$$ ， $$\mathbf{v}_i \in \mathbb{R}^{d_v}$$ 。注意力层接受一个查询向量 $$\mathbf{q} \in \mathbb{R}^{d_q}$$ ，并返回一个输出 $$\mathbf{o} \in \mathbb{R}^{d_v}$$ ，其形状与值向量 $$\mathbf{v}$$ 相同。

The attention layer measures the similarity between the query and the key using a score function $$\alpha$$ , which returns scores $$a_1, \dots, a_n$$ for keys $$\mathbf{k}_1, \dots, \mathbf{k}_n$$ given by:

注意力层使用一个评分函数 $$\alpha$$ 来计算查询向量与键向量之间的相似性，返回键 $$\mathbf{k}_1, \dots, \mathbf{k}_n$$ 的评分 $$a_1, \dots, a_n$$ ：

$$
a_i = \alpha(\mathbf{q}, \mathbf{k}_i)
$$

Attention weights are computed as a softmax function on the scores:

注意力权重通过对评分进行 Softmax 计算得到：

$$
\mathbf{b} = \text{softmax}(\mathbf{a})
$$

Each element of $$\mathbf{b}$$ is computed as follows:

向量 $$\mathbf{b}$$ 的每个元素计算如下：

$$
b_i = \frac{\exp(a_i)}{\sum_j \exp(a_j)}
$$

The output is the weighted sum of the attention weights and the values:

最终输出是注意力权重与值的加权求和：

$$
\mathbf{o} = \sum_{i=1}^{n} b_i \mathbf{v}_i
$$

### Scaled Dot-Product Attention (缩放点积注意力)

The score function $$\alpha(\mathbf{q}, \mathbf{k})$$ exists in various forms, leading to multiple types of attention mechanisms. The dot product-based scoring function is the simplest, requiring no tunable parameters. A variation, the scaled dot product, normalizes this by $$\sqrt{d_k}$$ to mitigate the impact of increasing dimensions (Luong et al., 2015; Vaswani et al., 2017).

评分函数 $$\alpha(\mathbf{q}, \mathbf{k})$$ 具有多种形式，导致了不同类型的注意力机制。基于点积的评分函数是最简单的，并不需要可调参数。一个变体是**缩放点积注意力**，它通过除以 $$\sqrt{d_k}$$ 进行归一化，以减小维度增加带来的影响（Luong et al., 2015; Vaswani et al., 2017）。

$$
\alpha(\mathbf{q}, \mathbf{k}) = \frac{\mathbf{q} \cdot \mathbf{k}}{\sqrt{d_k}}
$$

### Self-Attention (自注意力)

In self-attention, each input vector $$\mathbf{x}_i$$ is projected onto three distinct vectors: query $$\mathbf{q}_i$$, key $$\mathbf{k}_i$$, and value $$\mathbf{v}_i$$ . These projections are performed via learnable weight matrices $$\mathbf{W}_Q, \mathbf{W}_K, \mathbf{W}_V$$, resulting in:

在**自注意力**机制中，每个输入向量 $$\mathbf{x}_i$$ 被投影到三个不同的向量：查询向量 $$\mathbf{q}_i$$、键向量 $$\mathbf{k}_i$$ 和值向量 $$\mathbf{v}_i$$ 。这些投影由可学习的权重矩阵 $$\mathbf{W}_Q, \mathbf{W}_K, \mathbf{W}_V$$ 进行变换：

$$
\mathbf{q}_i = \mathbf{x}_i \mathbf{W}_Q, \quad \mathbf{k}_i = \mathbf{x}_i \mathbf{W}_K, \quad \mathbf{v}_i = \mathbf{x}_i \mathbf{W}_V
$$

These weight matrices are initialized randomly and optimized during training.

这些权重矩阵在训练过程中随机初始化并进行优化。

The simplified matrix representation with each of the query, key, and value matrices as a single computation is given by:

整个注意力机制的矩阵形式表达如下：

$$
\text{attention}(\mathbf{Q}, \mathbf{K}, \mathbf{V}) = \text{softmax} \left( \frac{\mathbf{Q} \mathbf{K}^T}{\sqrt{d_k}} \right) \mathbf{V}
$$

