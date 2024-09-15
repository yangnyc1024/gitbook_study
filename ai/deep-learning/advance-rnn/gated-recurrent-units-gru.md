# Gated Recurrent Units(GRU)

我们讨论了如何在循环神经网络中计算梯度， 以及矩阵连续乘积可以导致梯度消失或梯度爆炸的问题。 下面我们简单思考一下这种梯度异常在实践中的意义：

Mathematically, for a given time step $$𝑡$$, suppose that the input is a minibatch $$𝑋_𝑡∈𝑅^𝑛×𝑑$$ (number of examples $$=𝑛$$; number of inputs $$=𝑑$$) and the hidden state of the previous time step is $$𝐻𝑡−1∈𝑅𝑛×ℎ$$ (number of hidden units $$=ℎ$$). Then the reset gate $$𝑅𝑡∈𝑅𝑛×ℎ$$ and update gate $$𝑍_𝑡 \in 𝑅_𝑛 \times ℎ$$ are computed as follows:

$$𝑅_𝑡=𝜎(𝑋_𝑡𝑊_xr+𝐻_𝑡−1𝑊_hr+𝑏r),𝑍𝑡=𝜎(𝑋𝑡𝑊_xz+𝐻_{t-1}𝑊_hz+𝑏z),$$



where and $$𝑊_hr,𝑊_hz \in 𝑅^ℎ \times ℎ$$ are weight parameters and  $$b_r, b_z \in 𝑅^1×ℎ$$ are bias parameters.

#### Conclusion

Compared with LSTMs, GRUs achieve similar performance but tend to be lighter computationally. Generally, compared with simple RNNs, gated RNNS, just like LSTMs and GRUs, can better capture dependencies for sequences with large time step distances. GRUs contain basic RNNs as their extreme case whenever the reset gate is switched on. They can also skip subsequences by turning on the update gate.
