# Bidirectional Recurrent Neural Networks(BRNN)

## Bidirectional Recurrent Neural Networks (BRNN) | 双向递归神经网络 (BRNN)

#### 1. **What is BRNN? | 什么是 BRNN？**

**Bidirectional Recurrent Neural Networks (BRNN)** is an extension of traditional recurrent neural networks (RNNs) designed to improve the ability to capture dependencies in sequential data. While traditional RNNs process sequences in one direction (usually from past to future), **BRNNs process sequences in both forward and backward directions simultaneously**, which allows the network to capture context from both the past and the future. This is particularly useful for tasks where the entire context of the sequence is needed to make predictions, such as speech recognition, natural language processing, and machine translation.\
**双向递归神经网络 (BRNN)** 是传统递归神经网络 (RNN) 的扩展，旨在增强其捕捉顺序数据依赖关系的能力。传统 RNN 只能从一个方向（通常是从过去到未来）处理序列，而 **BRNN 同时从正向和反向处理序列**，这使得网络能够捕捉到来自过去和未来的上下文信息。这对需要完整上下文信息来进行预测的任务特别有用，如语音识别、自然语言处理和机器翻译。

#### 2. **How Does BRNN Work? | BRNN 是如何工作的？**

In a **Bidirectional RNN**, two separate RNNs are used:

1. One RNN processes the sequence in the **forward direction**, from the first element to the last.
2. The second RNN processes the sequence in the **backward direction**, from the last element to the first.

The hidden states from both the forward and backward passes are concatenated at each time step to create a combined hidden state that takes into account both past and future context. The output at each time step is based on this combined hidden state, allowing the model to make more informed predictions by leveraging information from both directions.\
在 **双向 RNN** 中，有两个独立的 RNN：

1. 一个 RNN 按 **正向** 处理序列，从第一个元素到最后一个元素。
2. 另一个 RNN 按 **反向** 处理序列，从最后一个元素到第一个元素。

在每个时间步上，正向和反向传递的隐藏状态被拼接在一起，形成一个综合的隐藏状态，考虑到过去和未来的上下文。每个时间步的输出基于这个综合的隐藏状态，使得模型能够利用来自两个方向的信息做出更准确的预测。

**BRNN Equations | BRNN 方程**

1. **Forward RNN**: The hidden state in the forward direction is computed as: $$h_t^{\text{forward}} = f(W_h \cdot h_{t-1}^{\text{forward}} + W_x \cdot x_t)$$ where:
   * $$h_t^{\text{forward}}$$ is the hidden state at time step $$t$$ in the forward RNN,
   * $$x_t$$ is the input at time step $$t$$,
   * $$W_h$$ and $$W_x$$ are weight matrices.
2. **Backward RNN**: The hidden state in the backward direction is computed as: $$h_t^{\text{backward}} = f(W_h \cdot h_{t+1}^{\text{backward}} + W_x \cdot x_t)$$
3. **Output**: The final hidden state at each time step is the concatenation of the forward and backward hidden states: $$h_t = [h_t^{\text{forward}}, h_t^{\text{backward}}]$$
4. **Final Output**: The output at time step $$t$$ is computed from the combined hidden state: $$y_t = W_y \cdot h_t$$

By combining the information from both directions, the network gains a better understanding of the input sequence, which helps in tasks that require context from both the past and future.

1. **正向 RNN**：正向 RNN 的隐藏状态计算如下： $$h_t^{\text{forward}} = f(W_h \cdot h_{t-1}^{\text{forward}} + W_x \cdot x_t)$$ 其中：
   * $$h_t^{\text{forward}}$$ 是时间步 $$t$$ 的正向隐藏状态，
   * $$x_t$$ 是时间步 $$t$$ 的输入，
   * $$W_h$$ 和 $$W_x$$ 是权重矩阵。
2. **反向 RNN**：反向 RNN 的隐藏状态计算如下： $$h_t^{\text{backward}} = f(W_h \cdot h_{t+1}^{\text{backward}} + W_x \cdot x_t)$$
3. **输出**：每个时间步的最终隐藏状态是正向和反向隐藏状态的拼接： $$h_t = [h_t^{\text{forward}}, h_t^{\text{backward}}]$$
4. **最终输出**：时间步 $$t$$ 的输出由综合隐藏状态计算得到： $$y_t = W_y \cdot h_t$$

通过结合来自两个方向的信息，网络能够更好地理解输入序列，这有助于那些需要同时利用过去和未来上下文的任务。

#### 3. **Advantages of BRNN | BRNN 的优势**

* **Access to Future Context | 获取未来上下文**: BRNNs can capture both past and future information simultaneously, which is crucial for tasks like speech recognition and language modeling, where the meaning of a word or phrase depends on the entire sequence. **获取未来上下文**：BRNN 可以同时捕捉到过去和未来的信息，这对于语音识别和语言建模等任务至关重要，因为单词或短语的含义通常依赖于整个序列。
* **Improved Accuracy | 提高精度**: By utilizing both forward and backward contexts, BRNNs often achieve higher accuracy on tasks that involve sequential data compared to traditional unidirectional RNNs. **提高精度**：通过利用正向和反向上下文，BRNN 在处理顺序数据的任务上通常比传统单向 RNN 获得更高的准确性。
* **Versatility | 多功能性**: BRNNs are widely used in tasks that require a comprehensive understanding of the input sequence, such as machine translation, part-of-speech tagging, and named entity recognition. **多功能性**：BRNN 广泛应用于需要全面理解输入序列的任务，如机器翻译、词性标注和命名实体识别。

#### 4. **Limitations of BRNN | BRNN 的局限性**

* **Increased Computational Cost | 计算成本增加**: Because BRNNs process sequences in both directions, they require more computational resources and memory compared to unidirectional RNNs. **计算成本增加**：由于 BRNN 同时处理正向和反向序列，因此它们比单向 RNN 需要更多的计算资源和内存。
* **Non-Causal Applications | 非因果应用**: BRNNs are typically not suitable for real-time applications where predictions need to be made immediately (e.g., online speech recognition), because the backward RNN requires access to the entire sequence before making predictions. **非因果应用**：BRNN 通常不适合需要立即做出预测的实时应用（如在线语音识别），因为反向 RNN 需要在做出预测之前访问整个序列。

#### 5. **Applications of BRNN | BRNN 的应用**

* **Speech Recognition | 语音识别**: BRNNs are widely used in speech recognition systems to capture both past and future context in spoken language, improving transcription accuracy. **语音识别**：BRNN 广泛用于语音识别系统中，通过捕捉语音中过去和未来的上下文来提高转录的准确性。
* **Natural Language Processing (NLP) | 自然语言处理**: BRNNs are commonly used in NLP tasks such as machine translation, sentiment analysis, and text classification, where understanding the context from both directions is important. **自然语言处理 (NLP)**：BRNN 常用于自然语言处理任务，如机器翻译、情感分析和文本分类，在这些任务中理解双向上下文至关重要。
* **Time Series Analysis | 时间序列分析**: BRNNs are effective in time series analysis, where future values might help predict the current state. **时间序列分析**：BRNN 在时间序列分析中表现出色，因为未来的值可能有助于预测当前状态。

#### 6. **BRNN with LSTM and GRU | BRNN 与 LSTM 和 GRU 的结合**

BRNN can be combined with more advanced RNN architectures like **LSTM** or **GRU** to further improve performance. This combination helps address the vanishing gradient problem while also capturing long-term dependencies from both directions.

* **Bidirectional LSTM (BiLSTM)**: Combines the power of LSTM’s gating mechanisms with bidirectional processing, making it effective for tasks requiring long-range dependencies and context from both directions.
* **Bidirectional GRU (BiGRU)**: A simpler version of BiLSTM, BiGRU uses GRU cells in both forward and backward directions, making it computationally more efficient while still benefiting from bidirectional context.

BRNN 可以与更先进的 RNN 架构（如 **LSTM** 或 **GRU**）结合使用，以进一步提高性能。这种组合有助于解决梯度消失问题，同时从双向捕捉长期依赖关系。

* **双向 LSTM (BiLSTM)**：结合了 LSTM 的门控机制与双向处理能力，使其在需要长程依赖和双向上下文的任务中表现出色。
* **双向 GRU (BiGRU)**：BiGRU 是 BiLSTM 的简化版，使用 GRU 单元进行正向和反向处理，在获得双向上下文的同时计算效率更高。

#### 7. **Example of BRNN in Action | BRNN 的操作示例**

Imagine using a **Bidirectional LSTM (BiLSTM)** for **sentiment analysis**:

1. The model receives a sentence as input and processes it both from the start to the end and from the end to the start.
2. The forward LSTM captures information about the earlier parts of the sentence, while the backward LSTM captures information about the later parts.
3. The hidden states from both the forward and backward LSTMs are combined at each word.
4. The final prediction of the sentiment (positive or negative) is based on the combined context from both directions.

In this case, BRNN (BiLSTM) allows the model to understand the sentiment based on the entire sentence, improving the accuracy of the prediction.\
以 **双向 LSTM (BiLSTM)** 用于 **情感分析** 为例：

1. 模型接收一个句子作为输入，并同时从头到尾和从尾到头处理它。
2. 正向 LSTM 捕捉句子前半部分的信息，而反向 LSTM 捕捉句子后半部分的信息。
3. 每个单词的正向和反向 LSTM 的隐藏状态被结合在一起。
4. 最终的情感预测（正面或负面）基于来自双向上下文的综合信息。

在这种情况下，BRNN (BiLSTM) 使模型能够基于整个句子理解情感，从而提高预测的准确性。

## Extra Reading

### Introduction

*   在序列学习中，我们以往假设的目标是： 在给定观测的情况下 （例如，在时间序列的上下文中或在语言模型的上下文中）， 对下一个输出进行建模。 虽然这是一个典型情景，但不是唯一的。 还可能发生什么其它的情况呢？ 我们考虑以下三个在文本序列中填空的任务。

    * 我`___`。
    * 我`___`饿了。
    * 我`___`饿了，我可以吃半头猪。

    根据可获得的信息量，我们可以用不同的词填空， 如“很高兴”（“happy”）、“不”（“not”）和“非常”（“very”）。 很明显，每个短语的“下文”传达了重要信息（如果有的话）， 而这些信息关乎到选择哪个词来填空， 所以无法利用这一点的序列模型将在相关任务上表现不佳。 例如，如果要做好命名实体识别 （例如，识别“Green”指的是“格林先生”还是绿色）， 不同长度的上下文范围重要性是相同的。 为了获得一些解决问题的灵感，让我们先迂回到概率图模型。
* 基本上来说，就是上下文可以帮助我们决定该词填什么

### 隐马尔可夫模型中的动态规划

* 如果我们想要用概率图来解决这个问题，可以引入一个隐变量，在任意的时间$$t$$, 我们假设存在某个隐变量$$h_t$$ ,从而我们透过概率 $$P(x_t \vert  h_t)$$ 可以帮助我们观察到 $$x_t$$。
* 同时，任何的$$h_t \rightarrow h_{t+1}$$,的状态，都是由一些转移概率 $$P(h_{t+1}\vert h_t)$$ 给出。
* 我们可以把这样的一个模型称为隐马尔可夫模型（hidden Markov model, hMM）
*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-09-12 at 9.46.02 PM.png" alt="" width="333"><figcaption></figcaption></figure>
* 所以，当我们把模型拓展到$$T$$  个观察值的时候，我们在观察状态和隐状态就有如下联合分布：$$P(x_1, \dots, x_T, h_1, \dots, h_T) = \prod_{t=1}^{T} P(h_t \mid h_{t-1}) P(x_t \mid h_t), \text{ where } P(h_1 \mid h_0) = P(h_1)$$
* 那么对应的前向递归（forward recursion）和反向递归（backward recursion）如下$$\pi_{t+1}(h_{t+1}) = \sum_{h_t} \pi_t(h_t) P(x_t \mid h_t) P(h_{t+1} \mid h_t)$$, $$\rho_{t-1}(h_{t-1}) = \sum_{h_t} P(h_t \mid h_{t-1}) P(x_t \mid h_t) \rho_t(h_t)$$
* 所以我们可以得到以下公式

$$P(x_j \mid x_{-j}) \propto \sum_{h_j} \pi_j(h_j) \rho_j(h_j) P(x_j \mid h_j)$$

* 前后递推都是线性 $$O(kT)$$, 是消息传递算法的体特例

### 双向模型

* 如果我们想要有类似于hMM的前瞻性，只需要增加一个“从最后一个词元开始从后向前运行”的RNN，去取代只有一个前向模式“从第一个词元开始运行”的RNN
* 双向循环神经网络(bidirectional RNNs)，添加了反向传递的隐藏层，可以更灵魂处理此类信息
*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-09-12 at 10.02.00 PM.png" alt="" width="320"><figcaption></figcaption></figure>

### 双向模型的定义

对于任意时间步 $$t$$，给定一个小批量的输入数据 $$\bm{X}_t \in \mathbb{R}^{n \times d}$$ （样本数 $$n$$，每个示例中的输入数 $$d$$），并且令隐藏层激活函数为 $$\phi$$。

在双向架构中，我们设该时间步的前向和反向隐藏状态分别为 $$\overrightarrow{\bm{H}}_t \in \mathbb{R}^{n \times h}$$ 和 $$\overleftarrow{\bm{H}}_t \in \mathbb{R}^{n \times h}$$，其中 $$h$$ 是隐藏单元的数目。前向和反向隐藏状态的更新如下：

$$\overrightarrow{\bm{H}}_t = \phi \left( \bm{X}_t \bm{W}_{xh}^{(f)} + \overrightarrow{\bm{H}}_{t-1} \bm{W}_{hh}^{(f)} + \bm{b}_h^{(f)} \right),$$&#x20;

$$\overleftarrow{\bm{H}}_t = \phi \left( \bm{X}_t \bm{W}_{xh}^{(b)} + \overleftarrow{\bm{H}}_{t+1} \bm{W}_{hh}^{(b)} + \bm{b}_h^{(b)} \right)$$

其中，权重 $$\bm{W}_{xh}^{(f)} \in \mathbb{R}^{d \times h}, \bm{W}_{hh}^{(f)} \in \mathbb{R}^{h \times h}, \bm{W}_{xh}^{(b)} \in \mathbb{R}^{d \times h}, \bm{W}_{hh}^{(b)} \in \mathbb{R}^{h \times h}$$ 和偏置 $$\bm{b}_h^{(f)} \in \mathbb{R}^{1 \times h}, \bm{b}_h^{(b)} \in \mathbb{R}^{1 \times h}$$ 都是模型参数。

接下来，将前向隐藏状态 $$\overrightarrow{\bm{H}}_t$$ 和反向隐藏状态 $$\overleftarrow{\bm{H}}_t$$ 连接起来，获得需要送入输出层的隐藏状态 $$\bm{H}_t \in \mathbb{R}^{n \times 2h}$$。在具有多个隐藏层的深度双向循环神经网络中，该信息作为输入传递到下一个双向层。最后，输出层计算得到的输出为 $$\bm{O}_t \in \mathbb{R}^{n \times q}$$（$$q$$ 是输出单元的数目）：

$$\bm{O}_t = \bm{H}_t \bm{W}_{hq} + \bm{b}_q,$$

这里，权重矩阵 $$\bm{W}_{hq} \in \mathbb{R}^{2h \times q}$$ 和偏置 $$\bm{b}_q \in \mathbb{R}^{1 \times q}$$ 是输出层的模型参数。事实上，这两个方向可以拥有不同数量的隐藏单元。

### Others

* 在Transformer模型之前，大多数最先进的NLP系统都依赖于诸如LSTM、门控循环单元（GRU）等门控RNN模型，并在此基础上增加了注意力机制。Transformer正是在注意力机制的基础上构建的，但其没有使用RNN结构，这表明仅依靠注意力机制就能在性能上比肩加上了注意力机制的RNN模型。
