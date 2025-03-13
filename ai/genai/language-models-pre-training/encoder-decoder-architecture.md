---
description: o
---

# Encoder-Decoder Architecture

## Encoder- Decoder Architecture

1. pivotal advancement in natural language processing, particularly in sequence- to sequence tasks such has machine translation, abstractive summarization, and question answering.
2. This framework is built upon two primary components: an encoder and a decoder.

### Encoder

The input text is tokenized into units(words or sub-words), which are then embedded into feature vectors $$x_1, x_2, \cdots, x_T$$.&#x20;

A unidirectional encoder updates its hidden state $$h_t$$ at each time $$t$$ using $$h_{t-1}$$ and $$x_t$$ as given by:

$$h_t = f(h_{t-1}, x_t)$$

The final state $$h_t$$ of the encoder is known as the context variable or the context vector, and it encodes the information of the entire input sequence and is given by:

$$c= m(h_1, \cdots, h_T)$$

where $$m$$ is the mapping function and, in the simplest case, maps the context variable to the last hidden state

$$c = m(h_1, \cdots, h_T) = h_T$$

Adding more complexity to the architecture, the encoders can be bidirectional; thus the hidden state would not only depend on the previous hidden state $$h_{t-1}$$ and input $$x_t$$, but also on the following state $$h_{t+1}$$



<figure><img src="../../.gitbook/assets/Screenshot 2025-03-09 at 11.53.55 PM.png" alt=""><figcaption></figcaption></figure>

hidden state是一个已知的所有的context vector，







### Decoder

Upon obtaining the context vector from the encoder, the decoder starts to generate the output sequence $$y = (y_1, y_2, \cdots, y_U)$$, where $$U$$ may differ from $$T$$. Similar to the encoder, the decoder's hidden state at any time $$t$$ is given by&#x20;

$$s_{t^{'}} = g(s_{t-1}, y_{t^{'} - 1}, c)$$

The hidden state of decoder flows to an output layer and the conditional distribution of the nxt token at $$t^{'}$$ is given by

$$P(y_{t'} | y_{t^{'} - 1}, \cdots, y_1, c) = \text{softmax} (s_{t-1}, y_{t^{'} - 1} , c)$$



\


### Encoder-Decoder Model Training and Loss Function

The encoder-decoder model is trained end-to-end through supervised learning. The standard loss function employed is the categorical cross-entropy between the predicted output sequence and the actual output. This can be represented as:

> 编码-解码模型通过监督学习进行端到端训练。标准损失函数是预测输出序列和实际输出之间的**分类交叉熵**。其数学表达式如下：

$$\mathcal{L} = - \sum_{t=1}^{U} \log p(y_t | y_{t-1}, \dots, y_1, \mathbf{c})$$

Optimization of the model parameters typically employs gradient descent variants, such as the Adam or RMSprop algorithms.

> 模型参数的优化通常采用梯度下降的变体，例如 **Adam** 或 **RMSprop** 算法。



## Issue

* Recurrent Neu- ral Networks (RNNs), the foundational architecture for many encoder-decoder mod- els, have shortcomings, such as susceptibility to <mark style="color:blue;">vanishing and exploding gradients</mark> (Hochreiter, 1998).&#x20;
* Additionally, the sequential dependency intrinsic to RNNs com- plicates parallelization, thereby imposing <mark style="color:blue;">computational constraints.</mark>

## Reference

* Large Language Models: A Deep Dive Chapter 2
