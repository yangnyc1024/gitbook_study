# Gated Recurrent Units(GRU)

Mathematically, for a given time step $$𝑡$$, suppose that the input is a minibatch $$𝑋𝑡∈𝑅𝑛×𝑑$$ (number of examples $$=𝑛$$; number of inputs $$=𝑑$$) and the hidden state of the previous time step is $$𝐻𝑡−1∈𝑅𝑛×ℎ$$ (number of hidden units $$=ℎ$$). Then the reset gate $$𝑅𝑡∈𝑅𝑛×ℎ$$ and update gate $$𝑍𝑡∈𝑅𝑛×ℎ$$ are computed as follows:

$$𝑅𝑡=𝜎(𝑋𝑡𝑊xr+𝐻𝑡−1𝑊hr+𝑏r),𝑍𝑡=𝜎(𝑋𝑡𝑊xz+𝐻𝑡−1𝑊hz+𝑏z),$$



where and $$𝑊hr,𝑊hz∈𝑅ℎ×ℎ$$ are weight parameters and $$𝑏r,𝑏z∈𝑅1×ℎ$$ are bias parameters.

#### Conclusion

Compared with LSTMs, GRUs achieve similar performance but tend to be lighter computationally. Generally, compared with simple RNNs, gated RNNS, just like LSTMs and GRUs, can better capture dependencies for sequences with large time step distances. GRUs contain basic RNNs as their extreme case whenever the reset gate is switched on. They can also skip subsequences by turning on the update gate.
