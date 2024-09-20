# Self-Attention

## Self-Attention | 自注意力机制

#### 1. **What is Self-Attention? | 什么是自注意力机制？**

**Self-Attention** is a type of attention mechanism used in neural networks, particularly in **Transformer models**, where each element in an input sequence attends to (or interacts with) every other element in the same sequence. The purpose of self-attention is to allow the model to understand relationships between different parts of the sequence, regardless of their position in the sequence.

Self-attention is especially useful in tasks where context matters, such as **machine translation**, **text summarization**, and **image processing**, because it helps the model capture both short-term and long-term dependencies between elements in the input.\
**自注意力机制** 是神经网络中的一种注意力机制，特别在 **Transformer 模型** 中广泛使用，它使输入序列中的每个元素可以关注（或与）同一序列中的其他元素进行交互。自注意力机制的目的是使模型能够理解序列中不同部分之间的关系，无论它们在序列中的位置如何。

自注意力机制在上下文信息重要的任务中非常有用，例如 **机器翻译**、**文本摘要** 和 **图像处理**，因为它帮助模型捕捉输入中元素之间的短期和长期依赖关系。

#### 2. **How Does Self-Attention Work? | 自注意力机制是如何工作的？**

The self-attention mechanism works by comparing each element in the input sequence to every other element and generating an output that is a weighted sum of all the elements. This process can be broken down into the following steps:

1. **Linear Projections (Query, Key, Value)**: For each element in the input sequence, the model creates three vectors: **Query (Q)**, **Key (K)**, and **Value (V)**. These vectors are created by applying learned linear transformations to the input embeddings. $$Q = W_Q \cdot X, \quad K = W_K \cdot X, \quad V = W_V \cdot X$$
2. **Calculate Attention Scores**: The attention score between a query and a key is calculated using the **dot product**. This score determines how much focus the query should give to the corresponding value. $$\text{score}(Q_i, K_j) = Q_i \cdot K_j$$
3. **Scaled Dot-Product Attention**: The attention scores are scaled by the square root of the dimension of the key vectors to prevent large values when the dimensionality is high. $$\text{scaled score}(Q_i, K_j) = \frac{Q_i \cdot K_j}{\sqrt{d_k}}$$
4. **Softmax to Get Attention Weights**: The scaled scores are passed through a **softmax** function to generate attention weights. These weights are then used to determine the importance of each key (and corresponding value) to the query. $$\alpha_{ij} = \text{softmax}\left(\frac{Q_i \cdot K_j}{\sqrt{d_k}}\right)$$
5. **Weighted Sum of Values**: The final output is computed as the **weighted sum** of the values, where the weights are the attention scores. $$\text{output}_i = \sum_j \alpha_{ij} V_j$$

This allows each element in the sequence to focus on (or attend to) the most relevant parts of the sequence, enabling the model to capture dependencies across the entire sequence.\
自注意力机制通过比较输入序列中的每个元素与其他元素，生成一个所有元素的加权和输出。其过程可以分为以下几个步骤：

1. **线性投影 (查询、键和值)**： 对于输入序列中的每个元素，模型创建三个向量：**查询 (Q)**、**键 (K)** 和 **值 (V)**。这些向量通过对输入嵌入应用线性变换来创建。 $$Q = W_Q \cdot X, \quad K = W_K \cdot X, \quad V = W_V \cdot X$$
2. **计算注意力得分**： 通过 **点积** 计算查询和键之间的注意力得分。这个得分决定了查询对相应值应给予多少关注。 $$\text{score}(Q_i, K_j) = Q_i \cdot K_j$$
3. **缩放点积注意力**： 注意力得分除以键向量维度的平方根进行缩放，以防止在高维度情况下得分过大。 $$\text{scaled score}(Q_i, K_j) = \frac{Q_i \cdot K_j}{\sqrt{d_k}}$$
4. **Softmax 计算注意力权重**： 缩放后的得分通过 **softmax** 函数生成注意力权重。使用这些权重来确定每个键（及其对应的值）对查询的重要性。 $$\alpha_{ij} = \text{softmax}\left(\frac{Q_i \cdot K_j}{\sqrt{d_k}}\right)$$
5. **值的加权和**： 最终输出是值的 **加权和**，其中权重是注意力得分。 $$\text{output}_i = \sum_j \alpha_{ij} V_j$$

通过这种方式，序列中的每个元素可以关注序列中最相关的部分，使模型能够捕捉整个序列中的依赖关系。

#### 3. **Why Use Self-Attention? | 为什么使用自注意力机制？**

* **Capture Dependencies Across the Sequence | 捕捉整个序列中的依赖关系**: Self-attention allows the model to capture relationships between different elements in the input sequence, regardless of how far apart they are. This makes it more powerful than traditional RNNs or CNNs for tasks involving long-range dependencies. **捕捉整个序列中的依赖关系**：自注意力机制使得模型能够捕捉输入序列中不同元素之间的关系，无论它们之间相距多远。这使得它比传统的 RNN 或 CNN 在处理涉及长期依赖关系的任务时更强大。
* **Parallelization | 并行化处理**: Unlike RNNs, which process sequences step by step, self-attention mechanisms allow for **parallel computation** since each element in the sequence can be processed independently. This greatly speeds up training and inference. **并行化处理**：与逐步处理序列的 RNN 不同，自注意力机制允许 **并行计算**，因为序列中的每个元素都可以独立处理。这大大加快了训练和推理的速度。
* **Rich Context Understanding | 丰富的上下文理解**: By attending to all elements of the sequence, self-attention provides a richer understanding of the context, which is critical for tasks like language modeling, translation, and summarization. **丰富的上下文理解**：通过关注序列中的所有元素，自注意力机制提供了对上下文的更丰富理解，这对于语言建模、翻译和摘要等任务至关重要。

#### 4. **Applications of Self-Attention | 自注意力机制的应用**

* **Machine Translation | 机器翻译**: Self-attention enables the model to focus on relevant parts of the input sentence, regardless of the distance between words, leading to more accurate translations. **机器翻译**：自注意力机制使模型能够关注输入句子中的相关部分，无论单词之间的距离如何，从而生成更准确的翻译。
* **Text Summarization | 文本摘要**: Self-attention helps in text summarization tasks by allowing the model to focus on key parts of the document and summarize important information. **文本摘要**：自注意力机制在文本摘要任务中帮助模型关注文档的关键部分，并总结出重要信息。
* **Question Answering | 问答系统**: In question-answering tasks, self-attention helps the model find the most relevant information in the text, leading to more accurate answers. **问答系统**：在问答任务中，自注意力机制帮助模型在文本中找到最相关的信息，从而提供更准确的答案。
* **Image Processing | 图像处理**: Self-attention is also applied in image processing tasks, where it helps the model focus on important regions of an image when generating descriptions or making decisions. **图像处理**：自注意力机制也应用于图像处理任务，帮助模型在生成描述或做出决策时关注图像的重要区域。

#### 5. **Self-Attention in Transformers | Transformer 中的自注意力机制**

In the **Transformer architecture**, self-attention is the foundation of both the **encoder** and **decoder**. The encoder uses self-attention to understand the relationships within the input sequence, while the decoder uses self-attention to understand the relationships within the output sequence generated so far. The self-attention mechanism allows the Transformer model to process entire sequences in parallel, making it highly efficient and effective for tasks like machine translation and text generation.\
在 **Transformer 架构** 中，自注意力机制是 **编码器** 和 **解码器** 的基础。编码器使用自注意力机制理解输入序列中的关系，而解码器使用自注意力机制理解已生成的输出序列中的关系。自注意力机制使 Transformer 模型能够并行处理整个序列，使其在机器翻译和文本生成等任务中既高效又有效。

**自注意力机制** 使序列中的每个元素都能够关注其他所有元素，无论它们之间的距离如何，从而捕捉依赖关系。其优势包括捕捉长程依赖关系、允许并行处理、提供更丰富的上下文理解。自注意力机制广泛应用于机器翻译、文本摘要、问答系统和图像处理等任务中。在 Transformer 模型中，自注意力机制是核心组件，支持序列的高效并行处理。

## Extra Reading

### Introduction

* 在深度学习里面，我们常会用到CNN和RNN对序列进行编码。想象一下，当我们有了注意力机制以后，我们可以将词元序列输入注意力池化中
  * 以至于我们可以在同一组词元同时充当查询，键，和值
  * 具体来说，就是每一个查询都会关注所有的键——值对，并且生成一个注意力的输出
  * 由于查询、键和值来自同一组输入，因此被称为 自注意力（self-attention） (Lin et al., 2017, Vaswani et al., 2017)， 也被称为内部注意力（intra-attention） (Cheng et al., 2016, Parikh et al., 2016, Paulus et al., 2017)。

### Self-Attention

给定一个由词元组成的输入序列 $$\mathbf{x}_1, \dots, \mathbf{x}_n$$，其中任意 $$\mathbf{x}_i \in \mathbb{R}^d \ (1 \leq i \leq n)$$。该序列的自注意力输出为一个长度相同的序列 $$\mathbf{y}_1, \dots, \mathbf{y}_n$$，其中：

* $$\mathbf{y}_i = f(\mathbf{x}_i, (\mathbf{x}_1, \mathbf{x}_n), \dots) \in \mathbb{R}^d$$
*

根据之前的定义的注意力汇聚函数 $$f$$。下面的代码片段是基于多头注意力对一个张量完成自注意力的计算，张量的形状为 (批量大小、时间步的数目或词元序列的长度，$$d$$)。输出与输入的张量形状相同。

### Comparing CNNs, RNNs, and Self-Attention

CNN,RNN, Self-Attention，目标都是将$$n$$个词元组成的序列映射到另一个长度相等的序列，其中的每个输入词元和输出词元都是由$$d$$维向量表示。

* 我们具体比较计算复杂性，顺序操作，和最大路径长度
* 注意顺序操作会妨碍并行计算，而任意的序列位置组合之间的路径越短，则能够越轻松地学习序列中的远距离的依赖关系



<figure><img src="../../../.gitbook/assets/Screenshot 2024-02-29 at 1.15.51 PM.png" alt="" width="375"><figcaption></figcaption></figure>

#### CNN

* 考虑一个卷积核大小为$$k$$的卷积层。 在后面的章节将提供关于使用卷积神经网络处理序列的更多详细信息。
* 目前只需要知道的是，由于序列长度是$$n$$，输入和输出的通道数量都是$$d$$， 所以卷积层的计算复杂度为$$O(knd^2)$$。因此卷积神经网络是分层的，因此为有$$O(1)$$个顺序操作， 最大路径长度为$$O(n/k)$$。 例如，图中卷积核大小为3的双层卷积神经网络的感受野内。

RNN

* 当更新循环神经网络的隐状态时， $$d \times d$$权重矩阵和$$d$$维隐状态的乘法计算复杂度为$$O(d^2)$$。 由于序列长度为$$n$$，因此循环神经网络层的计算复杂度为$$O(nd^2)$$。 根据图， 有$$O(n)$$个顺序操作无法并行化，最大路径长度也是$$O(n)$$。

#### Self Attention

* 在自注意力中，查询、键和值都是 $$n \times d$$ 矩阵。考虑缩放的“点-积”注意力，其中 $$n \times d$$ 矩阵乘以 $$d \times n$$ 矩阵。之后输出的 $$n \times n$$ 矩阵乘以 $$n \times d$$ 矩阵。因此，自注意力具有 $$\mathcal{O}(n^2 d)$$ 计算复杂性。
*   每个词元都通过自注意力直接连接到任何其他词元。因此，有 $$\mathcal{O}(1)$$ 个顺序操作可以并行计算，最大路径长度也是 $$\mathcal{O}(1)$$。

    总而言之，卷积神经网络和自注意力都有并行计算的优势，而且自注意力的最大路径长度最短。但是因为其计算复杂度是关于序列长度的二次方，所以在很长的序列中计算会非常慢。
* 总而言之，CNN和Self-Attention都拥有并行计算的优势。
* 在最大路径长度方面，Self-Attention的长度最短。但是因为其计算复杂度时关于序列长度的二次方，所以在很长的序列中计算会很慢

### Positional Encoding

* 在处理词元序列时，循环神经网络是逐个的重复地处理词元的， 而自注意力则因为并行计算而放弃了顺序操作。 为了使用序列的顺序信息，通过在输入表示中添加 _位置编码_（positional encoding）来注入绝对的或相对的位置信息。&#x20;
*   绝对位置信息


* 相对位置信息



