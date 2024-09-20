# The Transformer Architecture

## Transformer Architecture | Transformer 架构

#### 1. **What is the Transformer Architecture? | 什么是 Transformer 架构？**

The **Transformer architecture** is a deep learning model introduced by Vaswani et al. in the paper _"Attention is All You Need"_ (2017). It has become the foundation for many state-of-the-art models, such as **BERT**, **GPT**, and **T5**. The key innovation of the Transformer is its ability to model dependencies between input and output elements without relying on sequential processing, which was a limitation in traditional RNN-based models like LSTMs.

The Transformer uses **self-attention mechanisms** to capture relationships between elements in the input sequence, allowing for parallel processing and better handling of long-range dependencies. This architecture is primarily used in **natural language processing (NLP)** tasks like machine translation, text generation, and text summarization, but it has also been applied to areas like image processing and speech recognition.\
**Transformer 架构** 是由 Vaswani 等人在 2017 年的论文《Attention is All You Need》中提出的一种深度学习模型。它成为许多先进模型的基础，例如 **BERT**、**GPT** 和 **T5**。Transformer 的关键创新在于能够建模输入和输出元素之间的依赖关系，而不依赖于序列处理，这克服了传统基于 RNN 的模型（如 LSTM）的局限性。

Transformer 使用 **自注意力机制** 来捕捉输入序列中元素之间的关系，允许并行处理，并且更好地处理了长程依赖问题。该架构主要用于 **自然语言处理 (NLP)** 任务，如机器翻译、文本生成和文本摘要，但它也被应用于图像处理和语音识别等领域。

#### 2. **Key Components of the Transformer | Transformer 的关键组件**

The Transformer architecture consists of two main parts:

1. **Encoder**: Processes the input sequence and generates a set of continuous representations.
2. **Decoder**: Takes the encoder's output and generates the output sequence.

Both the encoder and decoder are made up of multiple layers, each containing two key sub-layers:

* **Self-Attention Mechanism**: Allows each position in the sequence to attend to all other positions, capturing dependencies across the sequence.
* **Feed-Forward Neural Network (FFNN)**: Applies a non-linear transformation to the attention outputs, enhancing the representation before passing it to the next layer.

Each layer also includes **residual connections** and **layer normalization**, which help stabilize training and improve gradient flow.\
Transformer 架构由两个主要部分组成：

1. **编码器**：处理输入序列并生成一组连续的表示。
2. **解码器**：接收编码器的输出并生成输出序列。

编码器和解码器都由多层组成，每层包含两个关键子层：

* **自注意力机制**：允许序列中的每个位置关注所有其他位置，从而捕捉序列中的依赖关系。
* **前馈神经网络 (FFNN)**：对注意力输出应用非线性变换，增强表示后传递给下一层。

每层还包括 **残差连接** 和 **层归一化**，它们有助于稳定训练并改善梯度流动。

**Encoder Structure | 编码器结构**

The encoder consists of multiple identical layers, each with two sub-layers:

1. **Self-Attention Layer**: Allows each word to attend to every other word in the sequence, capturing the dependencies between them.
2. **Feed-Forward Network**: A fully connected layer that applies non-linear transformations to the output of the attention layer.

Each layer has a residual connection around the two sub-layers, and **layer normalization** is applied after each sub-layer.\
编码器由多个相同的层组成，每层有两个子层：

1. **自注意力层**：允许序列中的每个单词关注序列中的其他单词，从而捕捉它们之间的依赖关系。
2. **前馈网络**：一个全连接层，对注意力层的输出应用非线性变换。

每层在两个子层之间有一个残差连接，并在每个子层之后应用 **层归一化**。

**Decoder Structure | 解码器结构**

The decoder also consists of multiple identical layers, but each layer has three sub-layers:

1. **Masked Self-Attention Layer**: Prevents the decoder from attending to future positions in the sequence during training (to avoid "cheating" by seeing the future).
2. **Encoder-Decoder Attention Layer**: Allows the decoder to attend to relevant parts of the encoder's output.
3. **Feed-Forward Network**: A fully connected layer applied to the output of the attention mechanism.

As in the encoder, each sub-layer is followed by residual connections and layer normalization.\
解码器同样由多个相同的层组成，但每层有三个子层：

1. **掩蔽自注意力层**：防止解码器在训练期间关注序列中的未来位置（以避免看到未来的信息“作弊”）。
2. **编码器-解码器注意力层**：允许解码器关注编码器输出中的相关部分。
3. **前馈网络**：一个全连接层，应用于注意力机制的输出。

与编码器一样，每个子层后面都有残差连接和层归一化。

#### 3. **Self-Attention in Transformers | Transformer 中的自注意力机制**

Self-attention is a critical mechanism in the Transformer that allows each word or token in a sequence to attend to other words or tokens, capturing dependencies between them. Unlike traditional RNNs or LSTMs, where information flows sequentially, self-attention allows the model to process all words simultaneously, enabling parallelization.

The process of **self-attention** involves three steps:

1. **Query, Key, and Value Projections**: Each word (or token) is projected into three vectors—**Query (Q)**, **Key (K)**, and **Value (V)**—using learned weight matrices. $$Q = W_Q \cdot X, \quad K = W_K \cdot X, \quad V = W_V \cdot X$$
2. **Attention Scores Calculation**: The attention score between each query and key is computed using the **dot product**, and then scaled to prevent large values when the dimensionality is high. $$\text{score}(Q, K) = \frac{Q \cdot K^T}{\sqrt{d_k}}$$
3. **Softmax and Weighted Sum**: The attention scores are passed through a **softmax** function to compute attention weights, which are then applied to the values to produce the output. $$\alpha = \text{softmax}\left(\frac{Q \cdot K^T}{\sqrt{d_k}}\right), \quad \text{output} = \alpha \cdot V$$

This allows the model to weigh the importance of different words in the sequence, helping it capture dependencies across the entire sequence.\
自注意力机制是 Transformer 中的关键机制，它允许序列中的每个单词或标记关注其他单词或标记，捕捉它们之间的依赖关系。与传统的 RNN 或 LSTM 不同，自注意力机制允许模型同时处理所有单词，从而实现并行化。

**自注意力机制** 的过程包括三个步骤：

1. **查询、键和值的投影**：每个单词（或标记）通过学习的权重矩阵被投影为三个向量——**查询 (Q)**、**键 (K)** 和 **值 (V)**。 $$Q = W_Q \cdot X, \quad K = W_K \cdot X, \quad V = W_V \cdot X$$
2. **计算注意力得分**：通过 **点积** 计算每个查询和键之间的注意力得分，然后进行缩放，以防止高维度下得分过大。 $$\text{score}(Q, K) = \frac{Q \cdot K^T}{\sqrt{d_k}}$$
3. **Softmax 和加权和**：将注意力得分通过 **softmax** 函数计算注意力权重，然后将这些权重应用于值以生成输出。 $$\alpha = \text{softmax}\left(\frac{Q \cdot K^T}{\sqrt{d_k}}\right), \quad \text{output} = \alpha \cdot V$$

这使得模型能够衡量序列中不同单词的重要性，从而帮助捕捉整个序列中的依赖关系。

#### 4. **Multi-Head Attention | 多头注意力机制**

The **Multi-Head Attention** mechanism extends self-attention by applying multiple attention mechanisms in parallel. Each "head" learns different aspects of the relationships in the input data, allowing the model to capture more complex patterns.

For each head, the input is projected into different sets of queries, keys, and values, and attention is applied separately. The outputs of all heads are concatenated and passed through a linear layer to generate the final output. $$\text{MultiHead}(Q, K, V) = \text{concat}(\text{head}_1, \dots, \text{head}_h)W_O$$

This helps the model focus on different parts of the input in parallel, improving its ability to understand complex dependencies.\
**多头注意力机制** 通过并行应用多个注意力机制扩展了自注意力。每个“头”学习输入数据关系的不同方面，从而使模型能够捕捉更复杂的模式。

对于每个头，输入被投影为不同的查询、键和值集合，并分别应用注意力。所有头的输出被拼接，并通过一个线性层生成最终输出。 $$\text{MultiHead}(Q, K, V) = \text{concat}(\text{head}_1, \dots, \text{head}_h)W_O$$

这有助于模型并行关注输入的不同部分，从而提高理解复杂依赖关系的能力。

#### 5. **Positional Encoding | 位置编码**

Since the Transformer does not rely on sequential processing, it lacks a natural way to encode the positions of words in the input sequence. To address this, **positional encoding** is added to the input embeddings to provide the model with information about the position of each word in the sequence.

Positional encodings are added to the word embeddings, and they are often based on sine and cosine functions of different frequencies: $$\text{PE}(pos, 2i) = \sin\left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right)$$ $$\text{PE}(pos, 2i+1) = \cos\left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right)$$

This allows the model to learn the order of the words and capture sequential information.\
由于 Transformer 不依赖序列处理，因此它缺乏一种自然的方式来编码输入序列中单词的位置。为了解决这一问题，**位置编码** 被添加到输入嵌入中，提供关于每个单词在序列中位置的信息。

位置编码被添加到单词嵌入中，通常基于不同频率的正弦和余弦函数： $$\text{PE}(pos, 2i) = \sin\left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right)$$ $$\text{PE}(pos, 2i+1) = \cos\left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right)$$

这使得模型能够学习单词的顺序并捕捉序列信息。

#### 6. **Applications of the Transformer Architecture | Transformer 架构的应用**

* **Machine Translation | 机器翻译**: Transformers are widely used in machine translation tasks, such as translating text between languages. The self-attention mechanism helps capture the dependencies between words across long distances. **机器翻译**：Transformer 广泛应用于机器翻译任务，如文本语言间的翻译。自注意力机制有助于捕捉长距离单词之间的依赖关系。
* **Text Generation | 文本生成**: Models like GPT (Generative Pretrained Transformer) are based on the Transformer architecture and are used for generating coherent text in tasks like dialogue generation, story completion, and code generation. **文本生成**：像 GPT（生成式预训练 Transformer）这样的模型基于 Transformer 架构，广泛用于生成连贯文本的任务，如对话生成、故事补全和代码生成。
* **Text Summarization | 文本摘要**: Transformers are used to generate summaries of long documents, allowing the model to focus on the most important sections of the text. **文本摘要**：Transformer 被用于生成长文档的摘要，使模型能够关注文本中最重要的部分。
* **Question Answering | 问答系统**: In question-answering systems, the Transformer architecture helps the model understand the context of the question and extract the relevant answer from the text. **问答系统**：在问答系统中，Transformer 架构帮助模型理解问题的上下文并从文本中提取相关答案。

#### Summary | 总结

* **Transformer** is a powerful architecture that uses self-attention mechanisms to capture relationships between elements in the input sequence, enabling parallel processing.
* **Key Components**: Encoder, decoder, self-attention, multi-head attention, and positional encoding.
* **Advantages**: Handles long-range dependencies, allows parallelization, and provides better context understanding.
* **Applications**: Machine translation, text generation, summarization, and question answering.

**Transformer** 是一种强大的架构，使用自注意力机制捕捉输入序列中元素之间的关系，从而实现并行处理。其关键组件包括编码器、解码器、自注意力、多头注意力和位置编码。Transformer 的优势在于能够处理长程依赖、支持并行化处理，并提供更好的上下文理解。应用领域包括机器翻译、文本生成、摘要和问答系统等。

## Extra Reading

* 值得注意的是，自注意力同时具有<mark style="color:purple;">并行计算</mark>和<mark style="color:purple;">最短的最大路径长度</mark>这两个优势。因此，使用自注意力来设计深度架构是很有吸引力的。
* 对比之前仍然依赖循环神经网络实现输入表示的自注意力模型 (Cheng et al., 2016, Lin et al., 2017, Paulus et al., 2017)，Transformer模型完全基于注意力机制，没有任何卷积层或循环神经网络层 (Vaswani et al., 2017)。
* 尽管Transformer最初是应用于在文本数据上的序列到序列学习，但现在已经推广到各种现代的深度学习中，例如语言、视觉、语音和强化学习领域。



### Transformer的架构

Transformer作为decoder-encoder的一个实例，可以看到其如下整体架构。

* 与Bahdanau注意力实现的seq-seq的学习相比，Transformer的编码器和解码器时基于自注意力的模块叠加而成。
* 源（输入）序列和目标（输出）序列的嵌入（embedding）表示将加上位置编码(position encoding)，再分别输入到decoder-encoder中

如图：

&#x20;                                                          ![](<../../../.gitbook/assets/Screenshot 2024-09-13 at 5.53.08 PM.png>)



#### Transformer的编码器

* 从宏观角度来看，Transformer的编码器是由多个相同的层叠加而成的，每个层都有两个子层（子层表示为$$sublayer$$sublayer。
  * 第一个子层是_<mark style="color:blue;">多头自注意力</mark>_<mark style="color:blue;">（multi-head self-attention）</mark>汇聚；
  * 第二个子层是_<mark style="color:orange;">基于位置的前馈网络</mark>_<mark style="color:orange;">（positionwise feed-forward network）</mark>。
  * 具体来说，在计算编码器的自注意力时，查询、键和值都来自前一个编码器层的输出。
* 自注意力时，查询、键和值都来自前一个编码器层的输出。
* 受 7.6 节中残差网络的启发，每个子层都采用了残差连接 (residual connection)。在 Transformer 中，对于序列中任何位置的任何输入 $$\mathbf{x} \in \mathbb{R}^d$$，都要求满足 $$sublayer(\mathbf{x}) \in \mathbb{R}^d$$，以便残差连接 $$\mathbf{x} + sublayer(\mathbf{x}) \in \mathbb{R}^d$$。
* 在残差连接的加法计算之后，紧接着应用层规范化 (layer normalization) (Ba et al., 2016)。
* 因此，输入序列对应的每个位置，Transformer 编码器都将输出一个 $$d$$ 维表示向量。



#### Transformers的解码器

* Transformer解码器也是由多个相同的层叠加而成的，并且层中使用了残差连接和层规范化。
* 除了编码器中描述的两个子层之外，解码器还在这两个子层之间插入了第三个子层，称为_编码器－解码器注意力_（encoder-decoder attention）层。
  * 在编码器－解码器注意力中，查询来自前一个解码器层的输出，而键和值来自整个编码器的输出。
  * 在解码器自注意力中，查询、键和值都来自上一个解码器层的输出。但是，解码器中的每个位置只能考虑该位置之前的所有位置。
  * 这种_掩蔽_（masked）注意力保留了_自回归_（auto-regressive）属性，确保预测仅依赖于已生成的输出词元。

### Part 0 基于缩放点积多头注意力 & 位置编码

这个在之前的章节已经提到过了

### Part 1基于位置的前馈网络

* 基于位置的前馈网络对序列中的所有位置的表示进行变换时使用的是同一个多层感知机（MLP），这就是称前馈网络是_基于位置的_（positionwise）的原因。
* 在实现中，输入`X`的形状（批量大小，时间步数或序列长度，隐单元数或特征维度）将被一个两层的感知机转换成形状为（批量大小，时间步数，`ffn_num_outputs`）的输出张量。
* 当改变张量的最里层维度的尺寸，会改变成基于位置的前馈网络的输出尺寸。因为用同一个多层感知机对所有位置上的输入进行变换，所以当所有这些位置的输入相同时，它们的输出也是相同的。

### Part 2残差连接和层规范化

* 现在让我们关注图中_加法和规范化_（add\&norm）组件。
* 正如在本节开头所述，这是由残差连接和紧随其后的层规范化组成的。两者都是构建有效的深度架构的关键。
* &#x20;在一个小批量的样本内基于批量规范化对数据进行重新中心化和重新缩放的调整
* 层规范化和批量规范化的目标相同，但层规范化是基于特征维度进行规范化。
* 尽管批量规范化在CV中被广泛应用，但是在NLP任务中（输入通常是变长序列）批量规范化通常不如层规范化的效果好



### Part 3编码器

* 当有了组成Transformer编码器的基础组件的时候，就可以先实现编码器的一个层，我们称它为EncoderBlocker，由残差连接和层规范化
* 在实现的Transformer编码器的代码中，堆叠了`num_layers`个`EncoderBlock`类的实例。由于这里使用的是值范围在$$−1$$和$$1$$之间的固定位置编码，因此通过学习得到的输入的嵌入表示的值需要先乘以嵌入维度的平方根进行重新缩放，然后再与位置编码相加。



### Part 4 解码器

* Transformer的解码器也是有多个相同的层组层
* 我们先从称为DecoderBlock类中实现，每个层包含了三个子层，
  * 解码器自注意力
  * Decoder-Encoder注意力
  * 基于位置的前馈网络
  * 这些子层也都被残差连接和紧随的层规范化和围绕
* 正如前面提到，在掩蔽多头解码器自注意力层(第一个子层)中，查询，键和值都是来自上一个解码器的输出
  * 关于Seq-to-Seq，在训练阶段，其输出序列的所有的位置(时间步)的词元都是已知的；
  * 然而在预测阶段，其输出序列的词元都是逐个生成的
* 因此，在任何解码器时间步中，只有生成的词元才能用于解码器的自注意力计算中。
  * 为了在解码器中保留自回归的属性，其掩蔽自注意力设定了参数dec\_valid\_lens,以便于任何查询都只会与解码器中所有已经生成词元的位置(既直到该查询位置为止)进行注意力计算。



## Summary

* Transformer是编码器－解码器架构的一个实践，尽管在实际情况中编码器或解码器可以单独使用。
* 在Transformer中，多头自注意力用于表示输入序列和输出序列，不过解码器必须通过掩蔽机制来保留自回归属性。
* Transformer中的残差连接和层规范化是训练非常深度模型的重要工具。
* Transformer模型中基于位置的前馈网络使用同一个多层感知机，作用是对所有序列位置的表示进行转换。