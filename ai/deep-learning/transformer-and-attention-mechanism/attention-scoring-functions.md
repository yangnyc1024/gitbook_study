# Attention Scoring Functions

As such, with the softmax operation to ensure nonnegative attention weights, much of the work has gone into _attention-scoring functions_ that are simpler to compute.



### Dot Production Attention



### Convenience Functions



### Scaled Dot Product Attention



### Additive Attention

* the _additive attention_ scoring function ([Bahdanau _et al._, 2014](https://d2l.ai/chapter\_references/zreferences.html#id10)) is given by $$\alpha(q, k) = w_v ^{T}tanh(W_qq W_kk) \in \mathbb{R}$$, where $$W_q \in \mathbb{R}^{h \times q}$$, $$W_k \in \mathbb{R}^{h\times k}$$and $$w_v \in \mathbb{R}^h$$ are the learnable parameters.
* This term is then fed into a softmax to ensure both nonnegativity and normalization.

