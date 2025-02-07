# The Transformer Architecture

## Introduction

* 值得注意的是，自注意力同时具有<mark style="color:purple;">并行计算</mark>和<mark style="color:purple;">最短的最大路径长度</mark>这两个优势。因此，使用自注意力来设计深度架构是很有吸引力的。
* 对比之前仍然依赖循环神经网络实现输入表示的自注意力模型 (Cheng et al., 2016, Lin et al., 2017, Paulus et al., 2017)，Transformer模型完全基于注意力机制，没有任何卷积层或循环神经网络层 (Vaswani et al., 2017)。
* 尽管Transformer最初是应用于在文本数据上的序列到序列学习，但现在已经推广到各种现代的深度学习中，例如语言、视觉、语音和强化学习领域。



## Transformer的架构

Transformer作为decoder-encoder的一个实例，可以看到其如下整体架构。

* 与Bahdanau注意力实现的seq-seq的学习相比，Transformer的编码器和解码器时基于自注意力的模块叠加而成。
* 源（输入）序列和目标（输出）序列的嵌入（embedding）表示将加上位置编码(position encoding)，再分别输入到decoder-encoder中

如图：

&#x20;                                                         &#x20;

<figure><img src="../../../.gitbook/assets/Screenshot 2024-09-13 at 5.53.08 PM.png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2024-09-20 at 12.21.21 AM.png" alt="" width="336"><figcaption></figcaption></figure>

#### Transformer的编码器

* 从宏观角度来看，Transformer的编码器是由多个相同的层叠加而成的，每个层都有两个子层（子层表示为$$sublayer$$sublayer。
  * 第一个子层&#x662F;_<mark style="color:blue;">多头自注意力</mark>_<mark style="color:blue;">（multi-head self-attention）</mark>汇聚；
  * 第二个子层&#x662F;_<mark style="color:orange;">基于位置的前馈网络</mark>_<mark style="color:orange;">（positionwise feed-forward network）</mark>。
  * 具体来说，在计算编码器的自注意力时，查询、键和值都来自前一个编码器层的输出。
* 自注意力时，查询、键和值都来自前一个编码器层的输出。
* 受 7.6 节中残差网络的启发，每个子层都采用了残差连接 (residual connection)。在 Transformer 中，对于序列中任何位置的任何输入 $$\mathbf{x} \in \mathbb{R}^d$$，都要求满足 $$sublayer(\mathbf{x}) \in \mathbb{R}^d$$，以便残差连接 $$\mathbf{x} + sublayer(\mathbf{x}) \in \mathbb{R}^d$$。
* 在残差连接的加法计算之后，紧接着应用层规范化 (layer normalization) (Ba et al., 2016)。
* 因此，输入序列对应的每个位置，Transformer 编码器都将输出一个 $$d$$ 维表示向量。



#### Transformers的解码器

* Transformer解码器也是由多个相同的层叠加而成的，并且层中使用了残差连接和层规范化。
* 除了编码器中描述的两个子层之外，解码器还在这两个子层之间插入了第三个子层，称&#x4E3A;_&#x7F16;码器－解码器注意力_（encoder-decoder attention）层。
  * 在编码器－解码器注意力中，查询来自前一个解码器层的输出，而键和值来自整个编码器的输出。
  * 在解码器自注意力中，查询、键和值都来自上一个解码器层的输出。但是，解码器中的每个位置只能考虑该位置之前的所有位置。
  * 这&#x79CD;_&#x63A9;蔽_（masked）注意力保留&#x4E86;_&#x81EA;回归_（auto-regressive）属性，确保预测仅依赖于已生成的输出词元。

### Part 0 基于缩放点积多头注意力 & 位置编码

这个在之前的章节已经提到过了

### Part 1基于位置的前馈网络Positionwise Feed-Forward Networks

* 基于位置的前馈网络对序列中的所有位置的表示进行变换时使用的是同一个多层感知机（MLP），这就是称前馈网络&#x662F;_&#x57FA;于位置的_（positionwise）的原因。
* 在实现中，输入`X`的形状（批量大小，时间步数或序列长度，隐单元数或特征维度）将被一个两层的感知机转换成形状为（批量大小，时间步数，`ffn_num_outputs`）的输出张量。
* 当改变张量的最里层维度的尺寸，会改变成基于位置的前馈网络的输出尺寸。因为用同一个多层感知机对所有位置上的输入进行变换，所以当所有这些位置的输入相同时，它们的输出也是相同的。

### Part 2残差连接和层规范化Residual Connection and Layer Normalization

* 现在让我们关注图&#x4E2D;_&#x52A0;法和规范化_（add\&norm）组件。
* 正如在本节开头所述，这是由残差连接和紧随其后的层规范化组成的。两者都是构建有效的深度架构的关键。
* &#x20;在一个小批量的样本内基于批量规范化对数据进行重新中心化和重新缩放的调整
* 层规范化和批量规范化的目标相同，但层规范化是基于特征维度进行规范化。
* 尽管批量规范化在CV中被广泛应用，但是在NLP任务中（输入通常是变长序列）批量规范化通常不如层规范化的效果好



### Part 3编码器Encoder

* 当有了组成Transformer编码器的基础组件的时候，就可以先实现编码器的一个层，我们称它为EncoderBlocker，由残差连接和层规范化
* 在实现的Transformer编码器的代码中，堆叠了`num_layers`个`EncoderBlock`类的实例。由于这里使用的是值范围在$$−1$$和$$1$$之间的固定位置编码，因此通过学习得到的输入的嵌入表示的值需要先乘以嵌入维度的平方根进行重新缩放，然后再与位置编码相加。



### Part 4 解码器Decoder

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
