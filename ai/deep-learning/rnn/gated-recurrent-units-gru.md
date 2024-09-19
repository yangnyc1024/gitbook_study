# Gated Recurrent Units(GRU)



## Gated Recurrent Units (GRU) | 门控循环单元 (GRU)

#### 1. **What is GRU? | 什么是 GRU？**

**Gated Recurrent Units (GRU)** is a type of recurrent neural network (RNN) architecture introduced by Kyunghyun Cho and colleagues in 2014. It is an improved version of the traditional RNN, designed to solve issues like **vanishing gradients** and to maintain information over longer sequences. GRU is simpler and computationally more efficient than the Long Short-Term Memory (LSTM) network, as it has fewer gates and parameters, making it a popular choice for sequential data tasks such as natural language processing and time series analysis.\
**门控循环单元 (GRU)** 是一种递归神经网络 (RNN) 架构，由 Kyunghyun Cho 等人在 2014 年提出。它是对传统 RNN 的改进，旨在解决诸如 **梯度消失** 等问题，并保持长时间序列中的信息。GRU 比长短期记忆网络 (LSTM) 更简单，计算效率更高，因为它具有更少的门控机制和参数，这使得 GRU 在处理自然语言处理和时间序列分析等顺序数据任务时非常流行。

#### 2. **How Does GRU Work? | GRU 是如何工作的？**

GRU introduces two key gates:

* **Reset Gate**: Determines how much of the past information should be forgotten.
* **Update Gate**: Controls how much of the new information should be added to the current state and how much of the previous state should be retained.

Unlike LSTM, GRU combines the forget and input gates into a single **update gate**, which simplifies the architecture and reduces the number of parameters. The GRU cell dynamically decides which information to keep or discard, making it more efficient in modeling long sequences.\
GRU 引入了两个关键的门控：

* **重置门**：决定应该遗忘多少过去的信息。
* **更新门**：控制应该向当前状态添加多少新信息，以及应该保留多少之前的状态。

与 LSTM 不同，GRU 将遗忘门和输入门合并为一个 **更新门**，这简化了架构并减少了参数数量。GRU 单元动态决定保留或丢弃哪些信息，这使得它在建模长序列时更加高效。

**GRU Equations | GRU 方程**

1. **Reset Gate**: Controls how much of the previous hidden state should be forgotten. $$r_t = \sigma(W_r \cdot [h_{t-1}, x_t])$$ where:
   * $$r_t$$ is the reset gate value,
   * $$h_{t-1}$$ is the previous hidden state,
   * $$x_t$$ is the current input,
   * $$W_r$$ are the weights of the reset gate,
   * $$\sigma$$ is the sigmoid function.
2. **Update Gate**: Determines the balance between the previous state and the candidate new state. $$z_t = \sigma(W_z \cdot [h_{t-1}, x_t])$$ where:
   * $$z_t$$ is the update gate value,
   * $$W_z$$ are the weights of the update gate.
3. **Candidate Hidden State**: Computes the new candidate hidden state based on the reset gate. $$\tilde{h}_t = \tanh(W_h \cdot [r_t \odot h_{t-1}, x_t])$$ where:
   * $$\tilde{h}_t$$ is the candidate hidden state,
   * $$\odot$$ denotes element-wise multiplication.
4. **Final Hidden State**: The final hidden state is a combination of the previous hidden state and the new candidate state, controlled by the update gate. $$h_t = (1 - z_t) \odot h_{t-1} + z_t \odot \tilde{h}_t$$

This mechanism allows the GRU to control the flow of information and effectively maintain long-term dependencies in the data.

1. **重置门**：控制之前的隐藏状态有多少应该被遗忘。 $$r_t = \sigma(W_r \cdot [h_{t-1}, x_t])$$ 其中：
   * $$r_t$$ 是重置门值，
   * $$h_{t-1}$$ 是前一个隐藏状态，
   * $$x_t$$ 是当前输入，
   * $$W_r$$ 是重置门的权重，
   * $$\sigma$$ 是 sigmoid 函数。
2. **更新门**：决定之前的状态和候选新状态之间的平衡。 $$z_t = \sigma(W_z \cdot [h_{t-1}, x_t])$$ 其中：
   * $$z_t$$ 是更新门值，
   * $$W_z$$ 是更新门的权重。
3. **候选隐藏状态**：基于重置门计算新的候选隐藏状态。 $$\tilde{h}_t = \tanh(W_h \cdot [r_t \odot h_{t-1}, x_t])$$ 其中：
   * $$\tilde{h}_t$$ 是候选隐藏状态，
   * $$\odot$$ 表示逐元素乘法。
4. **最终隐藏状态**：最终隐藏状态是之前隐藏状态和新候选状态的组合，由更新门控制。 $$h_t = (1 - z_t) \odot h_{t-1} + z_t \odot \tilde{h}_t$$

这种机制使 GRU 能够控制信息的流动，并有效保持数据中的长期依赖关系。

#### 3. **Comparison to LSTM | 与 LSTM 的比较**

* **Gates | 门控**: GRU has two gates (reset and update), while LSTM has three gates (forget, input, and output). This makes GRU simpler and faster to compute. **门控**：GRU 有两个门（重置和更新），而 LSTM 有三个门（遗忘、输入和输出）。这使得 GRU 更加简单，计算速度更快。
* **Performance | 性能**: GRU often performs similarly to LSTM on many tasks, but it is more computationally efficient due to its simpler structure. **性能**：在许多任务中，GRU 的表现与 LSTM 类似，但由于其结构更简单，计算效率更高。
* **Memory Efficiency | 内存效率**: GRU uses fewer parameters and less memory than LSTM, making it a good choice for resource-constrained environments. **内存效率**：GRU 使用的参数更少，内存效率更高，这使得它在资源受限的环境中是一个不错的选择。

#### 4. **Why Use GRU? | 为什么使用 GRU？**

* **Efficient for Long Sequences | 适用于长序列**: GRU is effective at handling long sequences of data, making it suitable for tasks like machine translation, speech recognition, and time series prediction. **适用于长序列**：GRU 能够有效处理长序列数据，适用于诸如机器翻译、语音识别和时间序列预测等任务。
* **Simpler and Faster than LSTM | 比 LSTM 更简单和快速**: GRU’s simpler structure with fewer gates makes it faster to train and requires fewer computational resources compared to LSTM. **比 LSTM 更简单和快速**：GRU 的结构更简单，门控更少，使其训练更快，所需计算资源比 LSTM 少。
* **Prevents Vanishing Gradients | 防止梯度消失**: Like LSTM, GRU addresses the vanishing gradient problem in traditional RNNs, allowing it to maintain long-term dependencies more effectively. **防止梯度消失**：与 LSTM 类似，GRU 解决了传统 RNN 中的梯度消失问题，使其能够更有效地保持长期依赖关系。

#### 5. **Applications of GRU | GRU 的应用**

* **Natural Language Processing (NLP) | 自然语言处理**: GRUs are widely used in tasks such as machine translation, language modeling, and text generation, where maintaining long-term dependencies is crucial. **自然语言处理 (NLP)**：GRU 广泛用于机器翻译、语言建模和文本生成等任务，在这些任务中，保持长期依赖关系至关重要。
* **Speech Recognition | 语音识别**: GRU is often used in speech recognition systems to model sequential audio data and capture long-term dependencies between sounds. **语音识别**：GRU 常用于语音识别系统中，以建模序列音频数据并捕捉声音之间的长期依赖关系。
* **Time Series Prediction | 时间序列预测**: GRU is effective in forecasting future data points in time series analysis, such as stock prices, weather patterns, or energy consumption. **时间序列预测**：GRU 在时间序列分析中有效预测未来数据点，如股票价格、天气模式或能源消耗。

#### 6. **Limitations of GRU | GRU 的局限性**

* **Not Always Better than LSTM | 并不总是优于 LSTM**: While GRU is more efficient in some cases, LSTM may outperform GRU on certain complex tasks where long-term dependencies are more critical. **并不总是优于 LSTM**：虽然 GRU 在某些情况下效率更高，但在一些长期依赖关系更为关键的复杂任务中，LSTM 可能表现更好。
* **Simpler Structure Can Be a Limitation | 简化的结构可能成为局限**: The reduced number of gates in GRU may limit its ability to control information flow as effectively as LSTM in highly complex tasks. **简化的结构可能成为局限**：GRU 中减少的门控数量可能会限制其在高度复杂任务中有效控制信息流的能力。

#### 7. **Example of GRU in Action | GRU 的操作示例**

Consider an example where a GRU model is used for **machine translation** from English to French:

1. The GRU receives a sequence of English words as input.
2. As each word is processed, the GRU updates its hidden state based on the previous hidden state and the current word, keeping track of the context.
3. The final hidden state is used to generate the French translation of the sentence.

In this case, GRU’s ability to maintain information over long sequences helps it retain the meaning of the sentence and produce accurate translations.\
以 GRU 模型用于 **机器翻译**（从英语到法语）为例：

1. GRU 接收一系列英语单词作为输入。
2. 在处理每个单词时，GRU 基于之前的隐藏状态和当前单词更新其隐藏状态，跟踪上下文。
3. 最终的隐藏状态用于生成句子的法语翻译。

在这种情况下，GRU 保持长序列信息的能力帮助它保留句子的含义并生成准确的翻译。

## Extra Reading

我们讨论了如何在循环神经网络中计算梯度， 以及矩阵连续乘积可以导致梯度消失或梯度爆炸的问题。 下面我们简单思考一下这种梯度异常在实践中的意义：

Mathematically, for a given time step $$𝑡$$, suppose that the input is a minibatch $$𝑋_𝑡∈𝑅^𝑛×𝑑$$ (number of examples $$=𝑛$$; number of inputs $$=𝑑$$) and the hidden state of the previous time step is $$𝐻𝑡−1∈𝑅𝑛×ℎ$$ (number of hidden units $$=ℎ$$). Then the reset gate $$𝑅𝑡∈𝑅𝑛×ℎ$$ and update gate $$𝑍_𝑡 \in 𝑅_𝑛 \times ℎ$$ are computed as follows:

$$𝑅_𝑡=𝜎(𝑋_𝑡𝑊_xr+𝐻_𝑡−1𝑊_hr+𝑏r),𝑍𝑡=𝜎(𝑋𝑡𝑊_xz+𝐻_{t-1}𝑊_hz+𝑏z),$$

where and $$𝑊_hr,𝑊_hz \in 𝑅^ℎ \times ℎ$$ are weight parameters and  $$b_r, b_z \in 𝑅^1×ℎ$$ are bias parameters.

#### Conclusion

Compared with LSTMs, GRUs achieve similar performance but tend to be lighter computationally. Generally, compared with simple RNNs, gated RNNS, just like LSTMs and GRUs, can better capture dependencies for sequences with large time step distances. GRUs contain basic RNNs as their extreme case whenever the reset gate is switched on. They can also skip subsequences by turning on the update gate.

**GRU** 是 LSTM 的简化版本，旨在高效处理顺序数据，同时解决梯度消失问题。**重置门和更新门** 控制信息在网络中的流动。GRU 的优势包括比 LSTM 更简单和快速、适用于长序列、计算效率高。GRU 广泛应用于自然语言处理、语音识别和时间序列预测等领域。
