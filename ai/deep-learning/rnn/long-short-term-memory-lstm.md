# Long Short-Term Memory(LSTM)



## Long Short-Term Memory (LSTM) | 长短期记忆网络 (LSTM)

#### 1. **What is LSTM? | 什么是 LSTM？**

**Long Short-Term Memory (LSTM)** is a type of recurrent neural network (RNN) architecture introduced by Sepp Hochreiter and Jürgen Schmidhuber in 1997. It is designed to overcome the limitations of traditional RNNs, particularly the **vanishing gradient problem**, which prevents RNNs from learning long-term dependencies. LSTMs use special **gates** to control the flow of information, allowing the network to remember information over long sequences and discard irrelevant information when necessary.\
**长短期记忆网络 (LSTM)** 是一种递归神经网络 (RNN) 架构，由 Sepp Hochreiter 和 Jürgen Schmidhuber 在 1997 年提出。LSTM 旨在克服传统 RNN 的局限性，尤其是 **梯度消失问题**，这会阻止 RNN 学习长期依赖关系。LSTM 使用特殊的 **门控机制** 来控制信息流动，使网络能够在长序列中记住信息，并在必要时丢弃无关信息。

#### 2. **How Does LSTM Work? | LSTM 是如何工作的？**

LSTM introduces **three gates** (input, forget, and output gates) and a **cell state** to regulate the information flow through the network.

* **Forget Gate**: Decides which information from the previous cell state should be forgotten.
* **Input Gate**: Determines what new information should be stored in the cell state.
* **Output Gate**: Controls what information from the current cell state should be passed to the output and the next hidden state.

These gates help the network selectively retain or discard information, making it effective at learning long-term dependencies.\
LSTM 引入了 **三个门**（输入门、遗忘门和输出门）以及一个 **细胞状态** 来调节网络中的信息流动。

* **遗忘门**：决定应该忘记前一个细胞状态中的哪些信息。
* **输入门**：决定哪些新信息应该存储在细胞状态中。
* **输出门**：控制从当前细胞状态中提取哪些信息作为输出并传递到下一个隐藏状态。

这些门控机制帮助网络有选择地保留或丢弃信息，使其能够有效学习长期依赖关系。

**LSTM Equations | LSTM 方程**

1. **Forget Gate**: Determines which parts of the previous cell state should be forgotten. $$f_t = \sigma(W_f \cdot [h_{t-1}, x_t] + b_f)$$ where:
   * $$f_t$$ is the forget gate value,
   * $$h_{t-1}$$ is the previous hidden state,
   * $$x_t$$ is the current input,
   * $$W_f$$ and $$b_f$$ are the forget gate weights and biases.
2. **Input Gate**: Controls which new information is stored in the cell state. $$i_t = \sigma(W_i \cdot [h_{t-1}, x_t] + b_i)$$ where:
   * $$i_t$$ is the input gate value.
3. **Candidate Cell State**: The candidate values for the cell state, created by a tanh activation. $$\tilde{C}_t = \tanh(W_C \cdot [h_{t-1}, x_t] + b_C)$$
4. **Cell State Update**: Combines the previous cell state with the new information. $$C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t$$ where:
   * $$C_t$$ is the updated cell state,
   * $$\odot$$ represents element-wise multiplication.
5. **Output Gate**: Controls what part of the cell state should be output as the hidden state. $$o_t = \sigma(W_o \cdot [h_{t-1}, x_t] + b_o)$$
6. **Final Hidden State**: The hidden state passed to the next time step. $$h_t = o_t \odot \tanh(C_t)$$

These equations allow the LSTM to store, update, and pass on information across long sequences.

1. **遗忘门**：决定前一个细胞状态中哪些部分应该被忘记。 $$f_t = \sigma(W_f \cdot [h_{t-1}, x_t] + b_f)$$ 其中：
   * $$f_t$$ 是遗忘门值，
   * $$h_{t-1}$$ 是前一个隐藏状态，
   * $$x_t$$ 是当前输入，
   * $$W_f$$ 和 $$b_f$$ 是遗忘门的权重和偏置。
2. **输入门**：控制哪些新信息存储在细胞状态中。 $$i_t = \sigma(W_i \cdot [h_{t-1}, x_t] + b_i)$$ 其中：
   * $$i_t$$ 是输入门值。
3. **候选细胞状态**：由 tanh 激活创建的候选细胞状态值。 $$\tilde{C}_t = \tanh(W_C \cdot [h_{t-1}, x_t] + b_C)$$
4. **细胞状态更新**：将前一个细胞状态与新信息结合。 $$C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t$$ 其中：
   * $$C_t$$ 是更新后的细胞状态，
   * $$\odot$$ 表示逐元素乘法。
5. **输出门**：控制从细胞状态中提取哪些信息作为输出。 $$o_t = \sigma(W_o \cdot [h_{t-1}, x_t] + b_o)$$
6. **最终隐藏状态**：传递到下一个时间步的隐藏状态。 $$h_t = o_t \odot \tanh(C_t)$$

这些方程使得 LSTM 能够在长序列中存储、更新和传递信息。

#### 3. **Why Use LSTM? | 为什么使用 LSTM？**

* **Handles Long-Term Dependencies | 处理长期依赖**: LSTM is effective at handling long-term dependencies, making it suitable for tasks where long-range context is important, such as language modeling and machine translation. **处理长期依赖**：LSTM 能够有效处理长期依赖关系，适用于需要长期上下文的重要任务，如语言建模和机器翻译。
* **Prevents Vanishing Gradients | 防止梯度消失**: LSTM's gating mechanisms help mitigate the vanishing gradient problem, which is common in traditional RNNs when dealing with long sequences. **防止梯度消失**：LSTM 的门控机制帮助缓解了传统 RNN 在处理长序列时常见的梯度消失问题。
* **Selective Information Retention | 选择性信息保留**: By using the forget and input gates, LSTM can decide which information to retain or discard, leading to more accurate predictions in sequential data tasks. **选择性信息保留**：通过遗忘门和输入门，LSTM 能够决定保留或丢弃哪些信息，从而在顺序数据任务中提供更准确的预测。

#### 4. **Comparison with GRU | 与 GRU 的比较**

* **Gates | 门控机制**: LSTM has three gates (forget, input, and output), while GRU has two gates (reset and update). LSTM is more complex and has more parameters than GRU. **门控机制**：LSTM 有三个门（遗忘、输入和输出），而 GRU 有两个门（重置和更新）。LSTM 比 GRU 更复杂，参数更多。
* **Performance | 性能**: LSTM tends to perform better on tasks where long-term dependencies are critical, while GRU is often more efficient in simpler tasks. **性能**：LSTM 在长期依赖关系关键的任务中表现更好，而 GRU 在简单任务中通常更高效。
* **Computation and Memory | 计算与内存**: LSTM requires more computational power and memory compared to GRU due to its additional gates. **计算与内存**：由于 LSTM 具有额外的门控机制，计算和内存需求比 GRU 更高。

#### 5. **Applications of LSTM | LSTM 的应用**

* **Natural Language Processing (NLP) | 自然语言处理**: LSTM is widely used in NLP tasks such as language modeling, machine translation, text generation, and sentiment analysis. **自然语言处理 (NLP)**：LSTM 广泛用于语言建模、机器翻译、文本生成和情感分析等 NLP 任务。
* **Speech Recognition | 语音识别**: LSTM is effective in capturing the temporal dependencies in speech data, making it useful in speech recognition systems. **语音识别**：LSTM 在捕捉语音数据的时间依赖性方面表现出色，使其在语音识别系统中具有很高的实用性。
* **Time Series Forecasting | 时间序列预测**: LSTM is commonly used in time series forecasting tasks, such as stock price prediction, weather forecasting, and energy consumption modeling. **时间序列预测**：LSTM 通常用于时间序列预测任务，如股票价格预测、天气预报和能源消耗建模。

#### 6. **Limitations of LSTM | LSTM 的局限性**

* **Computationally Expensive | 计算复杂**: LSTM has more parameters than traditional RNNs and GRU, making it slower to train and requiring more computational resources. **计算复杂**：LSTM 的参数比传统 RNN 和 GRU 多，使得训练速度较慢，且需要更多的计算资源。
* **Overfitting | 过拟合问题**: Due to the large number of parameters, LSTM models can sometimes overfit, especially when the dataset is small. **过拟合问题**：由于参数众多，LSTM 模型在数据集较小时可能会出现过拟合。

#### 7. **Example of LSTM in Action | LSTM 的操作示例**

Consider using LSTM for **language modeling**. The task is to predict the next word in a sentence:

1. The LSTM processes the input sequence of words one at a time.
2. The forget gate decides which parts of the previous state should be discarded.
3. The input gate determines which new information (the current word) should be added to the cell state.
4. The output gate decides which parts of the current cell state should be used to predict the next word.
5. The LSTM outputs a probability distribution over the possible next words based on the learned context.

In this case, the LSTM is able to capture the long-term dependencies within the sentence, allowing for accurate predictions of the next word.\
以 LSTM 用于 **语言建模** 为例。任务是预测句子中的下一个单词：

1. LSTM 逐个处理输入的单词序列。
2. 遗忘门决定前一个状态的哪些部分应该被丢弃。
3. 输入门决定应该将哪些新信息（当前单词）添加到细胞状态中。
4. 输出门决定应该使用细胞状态的哪些部分来预测下一个单词。
5. LSTM 根据学习到的上下文输出下一个单词的概率分布。

在这种情况下，LSTM 能够捕捉句子中的长期依赖关系，从而准确预测下一个单词。



**LSTM** 是一种强大的递归神经网络，旨在解决梯度消失问题并捕捉顺序数据中的长期依赖关系。它使用三个门（遗忘、输入和输出）来控制信息流动。LSTM 的优势包括处理长期依赖、预防梯度消失、选择性保留重要信息。LSTM 广泛应用于自然语言处理、语音识别和时间序列预测等领域。

## Extra Reading

The Long Short-Term Memory (LSTM) model is a type of Recurrent Neural Network (RNN) designed to handle the issue of vanishing gradients in traditional RNNs. The key idea behind LSTMs is to introduce memory cells that can store information for a long period of time, and gates that control the flow of information into and out of the memory cells.

An LSTM model consists of several components, including:

1. Input Gate: Determines how much of the new input should be stored in the memory cell.
2. Forget Gate: Controls how much of the previous memory should be forgotten.
3. Memory Cell: Acts as a container to store information over a long period of time.
4. Output Gate: Decides how much of the information in the memory cell should be output as the model's prediction.

Each of these components is modeled as a sigmoid neural network, where the output of each gate is between 0 and 1, representing the extent to which the corresponding operation is performed. The memory cell is updated based on the input, forget, and output gates, as well as the previous state of the cell.

LSTMs have proven to be very effective in various sequential data processing tasks, such as language modeling, speech recognition, and time series forecasting, due to their ability to store information for a long period of time, and selectively forget or update information as needed.



Reference

* [https://youtu.be/YCzL96nL7j0?feature=shared](https://youtu.be/YCzL96nL7j0?feature=shared)
