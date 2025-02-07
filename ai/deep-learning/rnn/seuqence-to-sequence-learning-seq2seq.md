# Seuqence to Sequence Learning(Seq2Seq)

## Sequence to Sequence Learning (Seq2Seq) | 序列到序列学习 (Seq2Seq)

#### 1. **What is Seq2Seq? | 什么是 Seq2Seq？**

**Sequence to Sequence (Seq2Seq) learning** is a framework used in deep learning for tasks where both the input and output are sequences, but the sequences can have different lengths. Seq2Seq models are widely used in applications such as **machine translation**, **text summarization**, **speech recognition**, and **image captioning**. The Seq2Seq architecture typically consists of two main components:

* **Encoder**: Encodes the input sequence into a fixed-size context vector.
* **Decoder**: Decodes the context vector into the output sequence.

This model architecture enables the transformation of input sequences (e.g., a sentence in one language) into output sequences (e.g., a sentence in another language) of varying lengths.\
**序列到序列 (Seq2Seq) 学习** 是一种深度学习框架，专用于输入和输出均为序列但长度可能不同的任务。Seq2Seq 模型广泛应用于 **机器翻译**、**文本摘要**、**语音识别** 和 **图像描述** 等领域。Seq2Seq 架构通常包括两个主要部分：

* **编码器**：将输入序列编码为固定大小的上下文向量。
* **解码器**：将上下文向量解码为输出序列。

这种模型架构能够将输入序列（如一种语言的句子）转换为不同长度的输出序列（如另一种语言的句子）。

#### 2. **How Does Seq2Seq Work? | Seq2Seq 是如何工作的？**

Seq2Seq models consist of two recurrent neural networks (RNNs), long short-term memory networks (LSTMs), or gated recurrent units (GRUs):

1. **Encoder**: The encoder processes the input sequence one token at a time and encodes the entire sequence into a fixed-size **context vector** (the final hidden state).
2. **Decoder**: The decoder takes the context vector and generates the output sequence, one token at a time, until it produces the **end-of-sequence** token.

**Encoder | 编码器**

The encoder is responsible for converting the input sequence (e.g., a sentence) into a compressed representation called the context vector. It uses a recurrent structure (such as RNN, LSTM, or GRU) to update its hidden state at each time step. After processing the entire input, the final hidden state serves as the context vector, summarizing the sequence.

For example, given an input sentence "The weather is nice today," the encoder converts this sentence into a fixed-size context vector representing its meaning.\
编码器负责将输入序列（如一个句子）转换为称为上下文向量的压缩表示。它使用递归结构（如 RNN、LSTM 或 GRU）在每个时间步更新其隐藏状态。处理完整个输入序列后，最终的隐藏状态作为上下文向量，概括了该序列的含义。

例如，给定输入句子 "The weather is nice today"，编码器将该句子转换为一个固定大小的上下文向量，代表其含义。

**Decoder | 解码器**

The decoder generates the output sequence one token at a time, using the context vector provided by the encoder. At each time step, the decoder produces a word or token, which is passed to the next time step as input, until the sequence is complete. The decoder is often trained using **teacher forcing**, where the true output from the training data is used as the next input during training.

For example, if the task is machine translation, the decoder will take the context vector and generate the translated sentence, such as "Il fait beau aujourd'hui" in French.\
解码器逐步生成输出序列，使用编码器提供的上下文向量。在每个时间步，解码器生成一个词或标记，并将其传递给下一个时间步作为输入，直到序列完成。解码器通常使用 **教师强制** 进行训练，在训练过程中使用真实输出作为下一个输入。

例如，如果任务是机器翻译，解码器将接收上下文向量并生成翻译后的句子，如法语句子 "Il fait beau aujourd'hui"。

#### 3. **Applications of Seq2Seq | Seq2Seq 的应用**

* **Machine Translation | 机器翻译**: Seq2Seq models are widely used for translating text from one language to another. For example, translating English sentences into French, Chinese, or other languages. **机器翻译**：Seq2Seq 模型广泛用于将文本从一种语言翻译为另一种语言。例如，将英语句子翻译为法语、中文或其他语言。
* **Text Summarization | 文本摘要**: Seq2Seq models can generate concise summaries from longer input documents, such as summarizing news articles or research papers. **文本摘要**：Seq2Seq 模型可以从较长的输入文档中生成简洁的摘要，例如对新闻文章或研究论文进行摘要。
* **Speech Recognition | 语音识别**: Seq2Seq is used to convert speech into text, where the input is a sequence of audio frames, and the output is a sequence of text tokens. **语音识别**：Seq2Seq 用于将语音转换为文本，其中输入是一系列音频帧，输出是一系列文本标记。
* **Image Captioning | 图像描述**: Seq2Seq models can generate captions for images, where the input is an image, and the output is a sequence of words describing the image. **图像描述**：Seq2Seq 模型可以为图像生成描述性文本，其中输入是图像，输出是一系列描述图像的单词。

#### 4. **Challenges in Seq2Seq | Seq2Seq 面临的挑战**

* **Fixed-Length Context Vector | 固定长度的上下文向量**: In the standard Seq2Seq architecture, the entire input sequence is compressed into a fixed-size context vector, which can lead to loss of information, especially for long sequences. This makes it difficult for the decoder to generate accurate outputs, especially when the input sequence is long and complex. **固定长度的上下文向量**：在标准 Seq2Seq 架构中，整个输入序列被压缩为一个固定大小的上下文向量，这可能导致信息丢失，尤其是在处理长序列时。这使得解码器难以生成准确的输出，尤其是当输入序列较长且复杂时。
* **Difficulty in Handling Long Sequences | 处理长序列的困难**: When dealing with long input sequences, Seq2Seq models may struggle to retain all relevant information in the fixed-length context vector, leading to reduced performance. **处理长序列的困难**：在处理长输入序列时，Seq2Seq 模型可能难以在固定长度的上下文向量中保留所有相关信息，从而导致性能下降。

#### 5. **Attention Mechanism in Seq2Seq | Seq2Seq 中的注意力机制**

To address the challenges associated with the fixed-length context vector, the **attention mechanism** was introduced. With attention, instead of relying on a single context vector, the decoder **dynamically focuses on different parts** of the input sequence at each time step. This allows the decoder to retrieve more relevant information from the encoder’s hidden states when generating the output.

In an attention-based Seq2Seq model, the decoder calculates a weighted sum of the encoder’s hidden states, where the weights are determined by how important each hidden state is for the current decoding step. This greatly improves the model’s ability to handle long and complex sequences.\
为了解决与固定长度上下文向量相关的挑战，引入了 **注意力机制**。通过注意力机制，解码器不再依赖单一的上下文向量，而是能够在每个时间步 **动态关注** 输入序列的不同部分。这使得解码器在生成输出时能够从编码器的隐藏状态中提取更相关的信息。

在基于注意力的 Seq2Seq 模型中，解码器通过加权求和计算编码器的隐藏状态，其中权重根据每个隐藏状态对当前解码步骤的重要性确定。这大大提高了模型处理长序列和复杂序列的能力。

#### 6. **Seq2Seq with Attention: Example | 带有注意力机制的 Seq2Seq 示例**

Consider an example of **machine translation** using a Seq2Seq model with attention:

1. The **encoder** processes the input sentence in English, such as "I love learning," and encodes it into hidden states.
2. The **attention mechanism** allows the decoder to focus on specific parts of the input sequence when generating each word of the output.
3. The **decoder** generates the French translation "J'aime apprendre" by dynamically attending to the most relevant hidden states at each time step.

Without attention, the model might struggle to accurately translate longer sentences, but with attention, it can focus on the relevant parts of the input sequence and produce more accurate translations.\
以 **机器翻译** 使用带有注意力机制的 Seq2Seq 模型为例：

1. **编码器** 处理英语输入句子，如 "I love learning"，并将其编码为隐藏状态。
2. **注意力机制** 使得解码器在生成每个输出单词时能够关注输入序列的特定部分。
3. **解码器** 通过动态关注每个时间步中最相关的隐藏状态，生成法语翻译 "J'aime apprendre"。

没有注意力机制，模型可能难以准确翻译长句子，但通过注意力机制，模型能够专注于输入序列的相关部分，并生成更准确的翻译。





**Seq2Seq** 是用于处理输入和输出长度不同的序列到序列任务（如机器翻译和文本摘要）的强大架构。其主要挑战是将输入压缩为固定长度的上下文向量，这会在处理长序列时变得困难。**注意力机制** 增强了 Seq2Seq 模型，使解码器能够动态关注输入序列的不同部分。Seq2Seq 的应用包括机器翻译、文本摘要、语音识别和图像描述等。



## Extra Reading

### Introduction

从上一个section里面我们知道，机器翻译的输入和输出序列都是长度可变的，为了解决这个问题，我们使用了decoder-ecoder模型，透过两个循环神经网络的编码器和解码器，透过一个hidden的中间层，将前后两个序列（语言）练习在一起，以至于我们可以用&#x4E8E;_&#x5E8F;列到序列_（sequence to sequence，seq2seq）类的学习任务

* 遵循decoder-ecoder的设计原则，RNN的编码器使用长度可以改变的序列作为输入，将其转换为固定形状的隐状态
* 为了可以连续生成输出的序列的词元，独立的RNN解码器是基于
  * 输入序列的编码信息
  * 已经看见的或者生成的词元来预测下一个词元
*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-09-12 at 11.43.41 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### Encoder

从技术上讲，编码器将长度可变的输入序列转换成形状固定的上下文变量$$c$$，并且将输入序列的信息在该上下文变量中进行编码, 可以使用循环神经网络来设计编码器:

* 考虑由一个序列组成的样本（批量大小=1）。假设输入序列是$$x_1, \ldots, x_T$$，其中$$x_t$$ 是输入文本序列中的第$$t$$个词元。
* 在时间步$$t$$，循环神经网络将词元$$x_t$$的输入特征向量$$x_t$$和$$h_{t-1}$$（即上一步的隐状态）转换为$$h_t$$（即当前步的隐状态）。使用一个函数$$f$$来描述循环神经网络的循环层所做的变换： $$h_t = f(x_t, h_{t-1})$$
* 总之，编码器通过选定的函数$$q$$，将所有时间步的隐状态转换为上下文变量： $$c = q(h_1, \ldots, h_T)$$比如，当选择$$q(h_1, \ldots, h_T) = h_T$$时，上下文变量仅仅是输入序列在最后时间步的隐状态$$h_T$$。

到目前为止，我们使用的是一个单向循环神经网络设计编码器，其中隐状态只依赖于输入子序列，这个子序列是由输入序列的起始位置到隐状态所在的时间步的位置（包括隐状态所在的时间步）组成。

我们也可以使用双向循环神经网络构造编码器，其中隐状态依赖于两个输入子序列，两个子序列是由隐状态所在的时间步之前的序列和之后的序列（包括隐状态所在的时间步），因此隐状态对整个序列的信息都进行了编码。

现在，让我们实现循环神经网络编码器。

* 注意，我们使用了嵌入层（embedding layer）来获得输入序列中每个词元的特征向量。嵌入层的权重是一个矩阵，其行数等于输入词表的大小（vocab\_size），其列数等于特征向量的维度（embed\_size）。
* 对于任意词元的索引$$i$$，嵌入层获取权重矩阵的第$$i$$行（从0开始）以返回其特征向量。另外，本文选择了一个多层门控循环单元来实现编码器。

## Decoder

正如上文提到的，编码器输出的上下文变量$$c$$对整个输入序列$$x_1, \ldots, x_T$$进行编码。来自训练数据集的输出序列$$y_1, y_2, \ldots, y_T$$，对于每个时间步$$t'$$（与输入序列或编码器的时间步$$t$$不同），解码器输出$$y_{t'}$$的概率取决于先前的输出子序列$$y_1, \ldots, y^{t'-1}$$和上下文变量$$c$$，即$$P(y_{t'} \mid y_1, \ldots, y^{t'-1}, c)$$。

为了在序列上模型化这种条件概率，我们可以使用另一个循环神经网络作为解码器。

* 在输出序列上的任意时间步$t'$，循环神经网络将来自上一步时间步的输出$$y_{t'-1}$$\
  和上下文变量$$c$$作为其输入，然后在当前时间步将它们和上一隐状态$$s_{t'-1}$$转换为隐状态$$s_{t'}$$。因此，可以使用函数$$g$$来表示解码器的隐藏层的变换： $$s_{t'} = g(y_{t'-1}, c, s_{t'-1})$$
* 在获得解码器的隐状态之后，我们可以使用输出层和softmax操作来计算在时间步$$t'$$$时输出$$y_{t'}$$的条件概率分布$$P(y_{t'} \mid y_1, \ldots, y^{t'-1}, c)$$。

当实现解码器时，我们直接使用编码器最后一个时间步的隐状态初始化解码器的隐状态。这就要求使用循环神经网络实现的编码器和解码器具有相同数量的层和隐藏单元。为了进一步包含经过编码的输入序列的信息，上下文变量在所有的时间步与解码器的输入进行拼接（concatenate）。为了预测输出词元的概率分布，在循环神经网络解码器的最后一层使用全连接层来变换隐状态。
