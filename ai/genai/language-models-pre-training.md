# Language Models Pre-training

## Encoder- Decoder Architecture

1. pivotal advancement in natural language processing, particularly in sequence- to sequence tasks such has machine translation, abstractive summarization, and question answering.
2. This framework is built upon two primary components: an encoder and a decoder.

### Encoder

The input text is tokenized into units(words or sub-words), which are then embedded into feature vectors $$x_1, x_2, \cdots, x_T$$.&#x20;

A unidirectional encoder updates its hidden state $$h_t$$ at each time $$t$$ using $$h_{t-1}$$ and $$x_t$$ as given by:

$$h_t = f(h_{t-1}, x_t)$$

The final state $$h_t$$ of the encoder is known as the context variable or the context vector, and it encodes the information of the entire input sequence and is given by:

$$c= m(h_1, \cdots, h_T)$$













## Reference

* Large Language Models: A Deep Dive Chapter 2
