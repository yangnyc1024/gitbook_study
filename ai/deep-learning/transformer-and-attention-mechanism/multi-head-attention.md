# Multi-Head Attention



## Multi-Head Attention | 多头注意力机制

#### 1. **What is Multi-Head Attention? | 什么是多头注意力机制？**

**Multi-Head Attention (MHA)** is a key component of the **Transformer** architecture, and it extends the traditional **self-attention mechanism** by applying attention multiple times in parallel. Each attention mechanism is called a "head," and it allows the model to focus on different parts of the input sequence in each head. The outputs from all the attention heads are concatenated and combined to produce a final output.

The **Multi-Head Attention** mechanism helps the model learn various types of relationships between words (or tokens) in the input sequence. Each attention head can focus on different aspects of the data, capturing information such as **short-term dependencies** in one head and **long-term dependencies** in another, improving the model's overall ability to understand complex patterns.\
**多头注意力机制 (MHA)** 是 **Transformer** 架构的关键组成部分，它通过并行应用多次注意力机制扩展了传统的 **自注意力机制**。每个注意力机制称为一个“头”，允许模型在每个头中关注输入序列的不同部分。所有注意力头的输出拼接并组合，生成最终的输出。

**多头注意力机制** 帮助模型学习输入序列中词（或标记）之间的各种关系。每个注意力头可以专注于数据的不同方面，例如，一个头捕捉 **短期依赖关系**，另一个头捕捉 **长期依赖关系**，从而增强模型理解复杂模式的能力。

#### 2. **How Does Multi-Head Attention Work? | 多头注意力机制是如何工作的？**

Multi-Head Attention works by applying multiple **self-attention** mechanisms in parallel. The process can be broken down into the following steps:

1. **Linear Projections for Q, K, V**: For each head, the model applies different linear projections to the **query (Q)**, **key (K)**, and **value (V)** matrices. These projections are learned during training and allow each head to focus on different aspects of the input sequence. The linear transformations create multiple sets of queries, keys, and values. $$Q_h = W_Q^h \cdot Q, \quad K_h = W_K^h \cdot K, \quad V_h = W_V^h \cdot V$$
2. **Scaled Dot-Product Attention**: For each head, the dot product between queries and keys is calculated to determine attention scores. These scores are scaled by the square root of the dimension of the key vectors to avoid large values when the dimensionality is high. $$\text{score}(Q_h, K_h) = \frac{Q_h \cdot K_h^T}{\sqrt{d_k}}$$
3. **Softmax and Weighted Sum**: The scores are passed through a **softmax** function to obtain attention weights, which are applied to the corresponding values to produce the output for each head. $$\alpha_h = \text{softmax}\left(\frac{Q_h \cdot K_h^T}{\sqrt{d_k}}\right), \quad \text{output}_h = \alpha_h \cdot V_h$$
4. **Concatenation of Heads**: After the attention mechanism is applied for each head, the outputs from all heads are concatenated. $$\text{MultiHeadOutput} = \text{concat}(\text{output}_1, \text{output}_2, \dots, \text{output}_h)$$
5. **Final Linear Projection**: The concatenated output is passed through a final linear transformation to combine the results of the different heads into a single representation. $$\text{FinalOutput} = W_O \cdot \text{MultiHeadOutput}$$

This allows the model to capture different relationships and dependencies in parallel, providing a richer understanding of the input sequence.\
多头注意力机制通过并行应用多个 **自注意力机制** 来工作。其过程可以分为以下几个步骤：

1. **查询、键和值的线性投影**： 对于每个头，模型对 **查询 (Q)**、**键 (K)** 和 **值 (V)** 矩阵应用不同的线性投影。这些投影在训练过程中被学习，允许每个头关注输入序列的不同方面。线性变换生成多组查询、键和值。 $$Q_h = W_Q^h \cdot Q, \quad K_h = W_K^h \cdot K, \quad V_h = W_V^h \cdot V$$
2. **缩放点积注意力**： 对于每个头，计算查询与键之间的点积以确定注意力得分。为避免高维度下得分过大，得分除以键向量维度的平方根进行缩放。 $$\text{score}(Q_h, K_h) = \frac{Q_h \cdot K_h^T}{\sqrt{d_k}}$$
3. **Softmax 与加权和**： 将得分通过 **softmax** 函数以获得注意力权重，并将这些权重应用于相应的值，以生成每个头的输出。 $$\alpha_h = \text{softmax}\left(\frac{Q_h \cdot K_h^T}{\sqrt{d_k}}\right), \quad \text{output}_h = \alpha_h \cdot V_h$$
4. **注意力头的拼接**： 在每个头应用注意力机制后，将所有头的输出拼接在一起。 $$\text{MultiHeadOutput} = \text{concat}(\text{output}_1, \text{output}_2, \dots, \text{output}_h)$$
5. **最终线性投影**： 拼接后的输出通过一个最终的线性变换，合并不同头的结果，生成一个单一的表示。 $$\text{FinalOutput} = W_O \cdot \text{MultiHeadOutput}$$

这使得模型能够并行捕捉不同的关系和依赖性，从而更丰富地理解输入序列。

#### 3. **Why Use Multi-Head Attention? | 为什么使用多头注意力？**

* **Parallel Processing of Different Features | 并行处理不同特征**: Multi-Head Attention allows the model to focus on different parts of the input sequence simultaneously. Each head learns different features and relationships, such as short-term dependencies in one head and long-term dependencies in another. **并行处理不同特征**：多头注意力允许模型同时关注输入序列的不同部分。每个头学习不同的特征和关系，例如一个头学习短期依赖关系，另一个头学习长期依赖关系。
* **Richer Feature Representation | 更丰富的特征表示**: By having multiple heads, the model can learn more complex patterns in the data. Each head captures different aspects of the input, providing a richer understanding of the sequence. **更丰富的特征表示**：通过拥有多个头，模型可以在数据中学习更复杂的模式。每个头捕捉输入的不同方面，从而提供更丰富的序列理解。
* **Improved Generalization | 改善泛化能力**: The use of multiple heads helps prevent overfitting by allowing the model to capture diverse patterns and dependencies, improving its ability to generalize to new data. **改善泛化能力**：使用多个头有助于防止过拟合，因为模型能够捕捉多样化的模式和依赖关系，从而提高其对新数据的泛化能力。

#### 4. **Applications of Multi-Head Attention | 多头注意力的应用**

* **Machine Translation | 机器翻译**: In machine translation tasks, Multi-Head Attention allows the model to simultaneously focus on different parts of the input sentence when generating the translation. For example, one head may focus on syntactic structure while another focuses on word meaning. **机器翻译**：在机器翻译任务中，多头注意力允许模型在生成翻译时同时关注输入句子的不同部分。例如，一个头可能专注于句法结构，而另一个头则关注词义。
* **Text Summarization | 文本摘要**: Multi-Head Attention helps in text summarization by enabling the model to focus on different parts of the document while generating a summary. Each head can capture different themes or key ideas from the text. **文本摘要**：多头注意力有助于文本摘要，使模型在生成摘要时能够关注文档的不同部分。每个头可以从文本中捕捉不同的主题或关键思想。
* **Question Answering | 问答系统**: In question-answering tasks, Multi-Head Attention helps the model focus on relevant portions of the text to provide accurate answers. Different heads can attend to different sentences or paragraphs in the passage. **问答系统**：在问答任务中，多头注意力帮助模型关注文本中与问题相关的部分，从而提供准确的答案。不同的头可以关注段落或文章中的不同句子或段落。

#### 5. **Multi-Head Attention in Transformers | Transformer 中的多头注意力**

In the **Transformer** architecture, **Multi-Head Attention** is used in both the **encoder** and **decoder**. In the encoder, Multi-Head Attention allows the model to focus on different words or tokens within the input sentence, capturing dependencies between words. In the decoder, it helps the model attend to different parts of the input sentence while generating the output sequence.

Additionally, the **decoder** uses Multi-Head Attention to focus on different parts of the output sequence generated so far, enabling better context understanding and more accurate predictions.\
在 **Transformer** 架构中，**多头注意力** 被用于 **编码器** 和 **解码器** 中。在编码器中，多头注意力允许模型关注输入句子中的不同单词或标记，捕捉词与词之间的依赖关系。在解码器中，它帮助模型在生成输出序列时关注输入句子的不同部分。

此外，**解码器** 使用多头注意力机制关注到目前为止生成的输出序列的不同部分，从而更好地理解上下文并提供更准确的预测。



**多头注意力机制** 使模型能够多次并行应用注意力机制，关注输入序列的不同部分。其优势包括并行处理、更丰富的特征表示和改善的泛化能力。多头注意力机制广泛应用于机器翻译、文本摘要、问答系统等自然语言处理任务中。在 Transformer 中，多头注意力用于编码器和解码器中，以捕捉输入和输出序列中的依赖关系和上下文。

## Extra Reading

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
