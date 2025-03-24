# Transformers



## Encoder

* The encoder is responsible for processing the input sequence and compressing the information into a context or memory for the decoder.
* Each encoder layer comprises three main elements:
  * **Multi-Head Attention**: catch signal?
  * **Feed-Forward Neural Network:** applying nonlinear transformation
  * **Add & Norm**:&#x20;
    * stabilizing the activations by combining residual connections and layer normalization.
    * mitigating the vanishing gradient problem in the encoder(decoder)

## Decoder

* The decoder takes the context from the encoder and generates the output sequence
* It is also composed of multiple layers and has many commonalities with the encoder, but with minor changes:
  * **Masked Multi-Head Attention**: similar with multi-head attention, but with a masking mechanism to ensure that the prediction for a given word doesn't depend on future words in the sequence
  * **Encoder-Decoder Attention**: this layer allows the decoder to focus on relevant parts of the input sequence, leveraging the context provided by the encoder
  * **Feed-Forward Neural Network**: refines the attention vectors in perparation for generating the output sequence





## Tokenization and Representation

tokenization:&#x20;

* converts sentences into a machine-readable format
* each word in the sentence is treated as a distinct token in word-level tokenization
* vector representation, such as word embeddings
* subword-level approaches such as byte-pair encoding(BPE) or WordPiece often address the limitations of word-level tokenization.
  * unhappiness split into "un" and "happiness"



## Positional Encodings

**Transformer 模型本身是无序的**，它不像 RNN 或 CNN 那样天然地处理序列的顺序信息。

* Since the Transformer model processes all tokens in the input sequence in parallel, it does not have a built-in mechanism to account for the token positions or order.
* provide the relative position of the tokens in the sequence
* usually added to the unit embedding before they are fed into the Transformer model



InputEmbedding = WordEmbedding + PositionalEncoding

$$\text{PE}{(pos, 2i)} = \sin\left(\frac{pos}{10000^{\frac{2i}{d{\text{model}}}}}\right)$$

$$\text{PE}{(pos, 2i+1)} = \cos\left(\frac{pos}{10000^{\frac{2i}{d{\text{model}}}}}\right)$$

* $$pos$$ is the position of the token in the sequence,
* $$i$$ is the dimension index,
* $$d_{\text{model}}$$ is the dimension of the model.

## Multi-Head Attention

* Employs $$h$$ parallel self-attention heads, to enhance the model's representational capacity
  * the original transformer model, $$h = 8$$ heads were used to allow the model to capture various aspects and dependencies within the input data, such as grammar and tense in machine translation tasks
* query, key, and value

More details in [https://app.gitbook.com/o/8FWDZYZclCPDejXXnS5n/s/KLjYi16C9OsVCRdrTcrH/\~/changes/235/deep-learning/attention-mechanisms-and-transformers](../../deep-learning/attention-mechanisms-and-transformers/)&#x20;





## Position-Wise Feed-Forward Neural Network

* Following the attention mechanism, the next component in the architecture of the Transformer model is the feed-forward neural network.&#x20;
* Position-Wise FFN 处理的是 <mark style="color:purple;">**每个位置的非线性特征变换，从而补充注意力机制的能力**</mark>
* x -> Multi-Head Attention -> Add & Norm -> Position-Wise FFN -> Add & Norm

#### 为什么叫 "Position-Wise"?

因为 **每个位置的表示都是独立地送入同一个前馈网络处理的**，即：

* 你有一个序列（比如长度为 $$n$$），每个位置是一个向量 $$x_i \in R_d$$&#x20;
* 你对每个 $$x_i$$​ 都使用 **相同的前馈网络（参数共享）** 进行变换。
* 所以是 "Position-Wise"：**不涉及位置之间的交互**，只是逐位置地非线性变换。

#### 类比理解

你可以把它类比为在图像处理中对每个像素单独使用一个小型神经网络做颜色调整。位置之间不相互干扰，但都使用相同的网络。



**既然 Attention 那么强，为什么还需要 FFN？**

* Attention 的核心是**上下文建模**，不能替代非线性映射。
* FFN 能做复杂的特征变换（比如组合特征、抑制无效信息等），是神经网络表达力的体现。
* 多层堆叠 Attention 会引入大量参数和计算，但未必带来效果提升；Attention + FFN 的结构更简洁、收敛更快。

**与普通 FFN 区别？**

* 普通 FFN 对整体输入处理；Position-Wise FFN 是对序列中每个位置独立、共享参数地应用 FFN。

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-24 at 2.37.29 PM.png" alt=""><figcaption></figcaption></figure>

## Layer Normalization

* In a manner akin to ResNets, the Transformer model employs a residual connection where the input $$X$$ is added to the output $$Z$$
* This normalization procedure ensures that each layer’s activations have a zero mean and a unit variance.(说白了就是确保normal)
* For each hidden unit $$h_i$$, the layer normalization is formulated as:\
  $$h_i = \frac{g}{\sigma}(h_i - \mu)$$\
  where $$g$$ is the gain variable (often set to 1), $$\mu$$ is the mean calculated as\
  $$\mu = \frac{1}{H} \sum_{i=1}^{H} h_i$$\
  and $$\sigma$$ is the standard deviation computed as\
  $$\sigma = \sqrt{ \frac{1}{H} \sum_{i=1}^{H} (h_i - \mu)^2 }$$&#x20;
* The layer normalization technique minimizes $$\textit{covariate shift}$$, i.e., the gradient dependencies between layers, thus accelerating convergence by reducing the required iterations

## Masked Multi-Head Attention

* the decoder aims to predict the next token (word or character) in the sequence by considering both the encoder’s output and the tokens already seen in the target sequence.&#x20;
* The first layer of the decoder adopts a particular strategy: it only has access to the tokens that come before the token it is currently trying to predict.
* The masking is implemented using a particular weight matrix **M**. In this matrix, entries corresponding to future tokens in the sequence are set to $-\infty$, and those for previous tokens are set to 0.
* This masking is applied after calculating the dot product of the Query (**Q**) and Key (**K**T) matrices but before applying the softmax function. As a result, the softmax output for future tokens becomes zero, effectively masking them from consideration. This ensures that the decoder cannot peek into future tokens in the sequence, thereby preserving the sequential integrity required for tasks such as language translation.

$$
\textit{maskedAttention}(\mathbf{Q}, \mathbf{K}, \mathbf{V}) = \text{softmax} \left( \frac{\mathbf{Q} \mathbf{K}^\top + \mathbf{M}}{\sqrt{d_k}} \right) \mathbf{V}
$$

## Encoder-Decoder Attention

* The encoder-decoder attention mechanism serves as the bridge that connects the encoder and the decoder, facilitating the transfer of contextual information from the source sequence to the target sequence.
* the encoder-decoder attention layer works similarly to standard multi-head attention but with a critical difference: the **Queries (Q)** come from the current state of the decoder, while the **Keys (K)** and **Values (V)** are sourced from the output of the encoder.

## Transformer Variants



<figure><img src="../../.gitbook/assets/Screenshot 2025-03-24 at 2.39.38 PM.png" alt=""><figcaption></figcaption></figure>

### Normalization Methods



### Normalization Position



### Activation Functions



### Positional Embeddings



### Attention Mechanism



### Structural Modifications
