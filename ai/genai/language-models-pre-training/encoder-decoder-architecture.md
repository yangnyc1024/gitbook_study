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







## Reference

* Large Language Models: A Deep Dive Chapter 2
