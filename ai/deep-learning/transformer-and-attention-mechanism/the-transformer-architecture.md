# The Transformer Architecture

* 值得注意的是，自注意力同时具有并行计算和最短的最大路径长度这两个优势。因此，使用自注意力来设计深度架构是很有吸引力的。
* 对比之前仍然依赖循环神经网络实现输入表示的自注意力模型 (Cheng et al., 2016, Lin et al., 2017, Paulus et al., 2017)，Transformer模型完全基于注意力机制，没有任何卷积层或循环神经网络层 (Vaswani et al., 2017)。
* 尽管Transformer最初是应用于在文本数据上的序列到序列学习，但现在已经推广到各种现代的深度学习中，例如语言、视觉、语音和强化学习领域。



### Transformer的架构

#### Transformer的编码器

* 从宏观角度来看，Transformer的编码器是由多个相同的层叠加而成的，每个层都有两个子层（子层表示为$$sublayer$$）。
  * 第一个子层是_多头自注意力_（multi-head self-attention）汇聚；
  * 第二个子层是_基于位置的前馈网络_（positionwise feed-forward network）。具体来说，在计算编码器的自注意力时，查询、键和值都来自前一个编码器层的输出。
* 每个子层都采用了_残差连接_（residual connection）。
  * 在Transformer中，对于序列中任何位置的任何输入$$x \in \mathbb{R}^d$$，都要求满足$$sublayer(x)\in \mathbb{R}^d$$，以便残差连接满足$$x+sublayer(x)\in \mathbb{R}^d$$。
  * 在残差连接的加法计算之后，紧接着应用_层规范化_（layer normalization） (Ba _et al._, 2016)。
  * 因此，输入序列对应的每个位置，Transformer编码器都将输出一个$$d$$维表示向量。

#### Transformers的解码器

* Transformer解码器也是由多个相同的层叠加而成的，并且层中使用了残差连接和层规范化。
* 除了编码器中描述的两个子层之外，解码器还在这两个子层之间插入了第三个子层，称为_编码器－解码器注意力_（encoder-decoder attention）层。
  * 在编码器－解码器注意力中，查询来自前一个解码器层的输出，而键和值来自整个编码器的输出。
  * 在解码器自注意力中，查询、键和值都来自上一个解码器层的输出。但是，解码器中的每个位置只能考虑该位置之前的所有位置。
  * 这种_掩蔽_（masked）注意力保留了_自回归_（auto-regressive）属性，确保预测仅依赖于已生成的输出词元。





Summary

* Transformer是编码器－解码器架构的一个实践，尽管在实际情况中编码器或解码器可以单独使用。
* 在Transformer中，多头自注意力用于表示输入序列和输出序列，不过解码器必须通过掩蔽机制来保留自回归属性。
* Transformer中的残差连接和层规范化是训练非常深度模型的重要工具。
* Transformer模型中基于位置的前馈网络使用同一个多层感知机，作用是对所有序列位置的表示进行转换。
