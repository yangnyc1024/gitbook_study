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





## Multi-Head Attention



## Position-Wise Feed-Forward Neural Network



## Layer Normalization



## Masked Multi-Head Attention



## Encoder-Decoder Attention



## Transformer Variants

### Normalization Methods



### Normalization Position



### Activation Functions



### Positional Embeddings



### Attention Mechanism



### Structural Modifications
