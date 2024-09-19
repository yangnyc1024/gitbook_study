# Encoder-Decoder Architecture

## Extra Reading

In general sequence-to-sequence problems like machine translation, inputs and outputs are of varying lengths that are unaligned. The standard approach to handling this sort of data is to design an _encoder-decoder_ architecture consisting of two major components: an _encoder_ that takes a variable-length sequence as input, and a _decoder_ that acts as a conditional language model, taking in the encoded input and the leftwards context of the target sequence and predicting the subsequent token in the target sequence.

* 机器翻译是序列转换模型的一个核心问题， 其输入和输出都是长度可变的序列。
* 我们可以设计一个包含两个主要组件的架构：
* 第一个组件是一个_编码器_（encoder）
  * &#x20;它接受一个长度可变的序列作为输入， 并将其转换为具有<mark style="color:purple;">固定形状的编码状态</mark>。
  * 编码器通常由一系列的神经网络层组成，比如循环神经网络（RNN）、长短期记忆网络（LSTM）或卷积神经网络（CNN）。编码器负责处理输入数据，将其转换成一个固<mark style="color:purple;">定维度的隐含向量</mark>，捕捉输入序列中的语义信息。
* 第二个组件是_解码器_（decoder）
  * 它将<mark style="color:purple;">固定形状的编码状态</mark>映射到长度可变的序列。 这被称为_编码器-解码器_（encoder-decoder）架构
  * 解码器接收来自编码器的隐含向量，并生成输出序列。解码器与编码器的结构类似，通常也是由RNN、LSTM或CNN构成。解码器的任务是<mark style="color:purple;">从隐含表示中逐步生成目标序列</mark>
* 隐含向量（Context Vector / Latent Vector）
  * &#x20;编码器将输入序列转换为一个固定长度的向量，称为上下文向量。这个向量包含了输入序列的语义信息，解码器利用它来生成目标序列。
* 我们以英语到法语的机器翻译为例子
  * 比如说给定一个英文的输入序列，They are watching
  * 首先使用一个encoder和decoder，把这个输入的序列变成一个“状态”
  * 然后对这个状态进行解码，一个词元接着一个词元地生成翻译后的序列作为输出：IIs regordent

### Encoder

encoder takes variable-length sequences as input `X`

### Decoder



