# Encoder-Decoder Architecture

In general sequence-to-sequence problems like machine translation, inputs and outputs are of varying lengths that are unaligned. The standard approach to handling this sort of data is to design an _encoder-decoder_ architecture consisting of two major components: an _encoder_ that takes a variable-length sequence as input, and a _decoder_ that acts as a conditional language model, taking in the encoded input and the leftwards context of the target sequence and predicting the subsequent token in the target sequence.

* 机器翻译是序列转换模型的一个核心问题， 其输入和输出都是长度可变的序列。
* 我们可以设计一个包含两个主要组件的架构：
  * 第一个组件是一个_编码器_（encoder）： 它接受一个长度可变的序列作为输入， 并将其转换为具有<mark style="color:purple;">固定形状的编码状态</mark>。
  * 第二个组件是_解码器_（decoder）： 它将<mark style="color:purple;">固定形状的编码状态</mark>映射到长度可变的序列。 这被称为_编码器-解码器_（encoder-decoder）架构

### Encoder

encoder takes variable-length sequences as input `X`

### Decoder



