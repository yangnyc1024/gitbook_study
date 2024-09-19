# Recurrent Neural Networks(RNN)





#### Review

* 我们介绍了$$n$$元语法模型， 其中单词$$x_t$$在时间步$$t$$的条件概率仅取决于前面$$n-1$$个单词。 对于时间步$$t-(n-1)$$之前的单词， 如果我们想将其可能产生的影响合并到$$x_t$$上， 需要增加$$n$$，然而模型参数的数量也会随之呈指数增长， 因为词表$$|\mathcal{V}|$$需要存储$$|\mathcal{V}|^n$$个数字，&#x20;
* 因此与其将$$P(x_t | x_{t-1}, \cdots, x_1)$$模型化， 不如使用隐变量模型$$P(x_t|x_{t-1},\cdots, x_1) \approx P(x_t |h_{t-1})$$
* 其中$$h_{t-1}$$是_隐状态_（hidden state）， 也称为_隐藏变量_（hidden variable）， 它存储了到时间步$$t-1$$的序列信息。 通常，我们可以基于当前输入$$x_t$$和先前隐状态$$h_{t-1}$$ 来计算时间步$$t$$处的任何时间的隐状态：$$h_{t-1} = f(x_t, h_{t-1})$$
* 对于函数$$f$$，隐变量模型不是近似值。 毕竟$$h_t$$是可以仅仅存储到目前为止观察到的所有数据， 然而这样的操作可能会使计算和存储的代价都变得昂贵。

### Neural Networks without Hidden States[¶](https://d2l.ai/chapter\_recurrent-neural-networks/rnn.html#neural-networks-without-hidden-states)

* Let’s take a look at an MLP with a single hidden layer.&#x20;
* Let the hidden layer’s activation function be $$\phi$$. Given a minibatch of examples $$X \in \mathbb{R}^{n \times d }$$ with batch size $$n$$ and $$d$$ inputs, the hidden layer output $$H \in \mathbb{R}^{n \times h}$$ is calculated as

$$H = \phi(XW_{xh} + b_{h})$$

* In previous equation, We have the weight parameter $$W_{xh} \in \mathbb{R}^{d \times h}$$, the bias parameter $$b_h \in \mathbb{R}^{1\times h}$$, and the number of hidden units $$ℎ$$, for the hidden layer. So armed, we apply broadcasting uring the summation. Next, the hidden layer output $$H$$ is used as input of the output layer, which is given by

$$O = H W_{hq} +b _{q}$$

* where $$O \in \mathbb{R}^{n \times q}$$ is the output variable, $$W_{hq}  \in \mathbb{R}^{h \times q}$$ is the weight parameter, and $$b_q \times \mathbb{R}^{1 \times q}$$ is the bias parameter of the output layer. If it is a classification problem, we can use $$softmax(O)$$ to compute the probability distribution of the output categories.
* This is entirely analogous to the regression problem we solved previously in previous section, we omit details. Suffice it to say that we can pick feature-label pairs at random and learn the parameters of our network via automatic differentiation and stochastic gradient descent.

### Recurrent Neural Networks with Hidden States

* Assume that we have a minibatch of inputs $$X_t \in \mathbb{R}^{n \times d}$$ at time step $$t$$. In other words, for a minibatch of $$n$$ sequence examples, each row of $$X_t$$ corresponds to one example at time step $$t$$ from the sequence.&#x20;
* Next, denote by $$H_t \in \mathbb{R}^{n \times h}$$ the hidden layer output of time step $$H_{t-1}$$. Unlike with MLP, here we save the hidden layer output $$H_{t-1}$$ from the previous time step and introduce a new weight parameter $$W_{hh} \in \mathbb{R}^{h \times h}$$ to describe how to use the hidden layer output of the previous time step in the current time step.&#x20;
* Specifically, the calculation of the hidden layer output of the current time step is determined by the input of the current time step together with the hidden layer output of the previous time step:
  * &#x20;$$H_t = \phi(X_tW_{xh} + H_{t-1}W_{hh} + b_h)$$&#x20;
  * From the relationship between hidden layer outputs $$H_{t-1}$$ and $$H_{t-1}$$ of adjacent time steps, we know that these variables captured and retained the sequence’s historical information up to their current time step, just like the state or memory of the neural network’s current time step.
  * Therefore, such a hidden layer output is called a _hidden state_. Since the hidden state uses the same definition of the previous time step in the current time step, the computation of this is _recurrent_.







*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-14 at 12.59.49 PM.png" alt=""><figcaption></figcaption></figure>
* 在本例中，模型参数是$$W_{xh}$$和$$W_{hh}$$的拼接， 以及$$b_h$$的偏置，所有这些参数都来自之前的公式。当前时间步$$t$$的隐状态$$H_t$$ 将参与计算下一时间步$$t+1$$的隐状态$$H_{t+1}$$。 而且$$H_{t}$$还将送入全连接输出层， 用于计算当前时间步$$t$$的输出$$O_{t}$$。

\


### &#x20;基于循环神经网络的字符级语言模型

* 我们的目标是根据过去的和当前的词元预测下一个词元， 因此我们将原始序列移位一个词元作为标签。 Bengio等人首先提出使用神经网络进行语言建模 ([Bengio _et al._, 2003](https://zh.d2l.ai/chapter\_references/zreferences.html#id8))。&#x20;
* 设小批量大小为1，批量中的文本序列为“machine”。 为了简化后续部分的训练，我们考虑使用 _字符级语言模型_（character-level language model）， 将文本词元化为字符而不是单词。
*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-14 at 1.02.44 PM.png" alt=""><figcaption><p>输入为machin，输出为achine</p></figcaption></figure>

### 通过时间反向传播

* &#x20;循环神经网络中的前向传播相对简单。 _通过时间反向传播_（backpropagation through time，BPTT） ([Werbos, 1990](https://zh.d2l.ai/chapter\_references/zreferences.html#id182))实际上是循环神经网络中反向传播技术的一个特定应用。&#x20;
* 它要求我们将循环神经网络的计算图一次展开一个时间步， 以获得模型变量和参数之间的依赖关系。 然后，基于链式法则，应用反向传播来计算和存储梯度。 由于序列可能相当长，因此依赖关系也可能相当长。

#### Analysis of Gradients in RNNs循环神经网络的梯度分析

* Full Computation
* Truncating Time Steps
* Randomized Truncation
* Comparing Strategies

#### Backpropagation Through Time in Detail
