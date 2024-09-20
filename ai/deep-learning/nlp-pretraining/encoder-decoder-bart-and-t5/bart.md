---
description: BART
---

# BART

### BART (Bidirectional and Auto-Regressive Transformers) | 双向和自回归的 Transformer (BART)

#### 1. **What is BART? | 什么是 BART？**

**BART (Bidirectional and Auto-Regressive Transformers)** is a pre-trained language model developed by Facebook AI in 2019. It combines both **bidirectional** and **autoregressive** properties, making it a highly flexible and powerful model for a wide range of natural language processing (NLP) tasks, including **text summarization**, **machine translation**, and **question answering**.

BART can be seen as a generalization of **BERT** and **GPT**, as it combines the best of both worlds:

* Like **BERT**, it is **bidirectional**, meaning it looks at the entire input sequence simultaneously.
* Like **GPT**, it is **autoregressive**, meaning it can generate text by predicting the next token in a sequence.

BART is specifically designed for sequence-to-sequence (seq2seq) tasks, where the input and output are sequences, and is effective in both **text generation** and **understanding** tasks.\
**BART（双向和自回归的 Transformer）** 是 Facebook AI 于 2019 年开发的预训练语言模型。它结合了 **双向** 和 **自回归** 的特性，使其成为适用于广泛自然语言处理（NLP）任务的强大模型，包括 **文本摘要**、**机器翻译** 和 **问答系统**。

BART 可以被看作是 **BERT** 和 **GPT** 的泛化，因为它结合了二者的优点：

* 像 **BERT** 一样，它是 **双向的**，这意味着它可以同时查看整个输入序列。
* 像 **GPT** 一样，它是 **自回归的**，这意味着它可以通过预测序列中的下一个标记来生成文本。

BART 特别设计用于序列到序列（seq2seq）任务，其中输入和输出都是序列，且在 **文本生成** 和 **理解** 任务中都表现出色。

#### 2. **How Does BART Work? | BART 是如何工作的？**

BART is an encoder-decoder model, similar to architectures used in **machine translation** systems. The encoder processes the input sequence, while the decoder generates the output sequence. BART is trained by **corrupting the input data** (like randomly masking words or sentences) and then learning to **reconstruct the original input**, similar to a denoising autoencoder.

**Encoder-Decoder Structure | 编码器-解码器结构**

* **Encoder**: The encoder takes in the corrupted input (where parts of the input have been altered or removed) and processes it to capture useful information.
* **Decoder**: The decoder takes the encoded representation and reconstructs the original text by predicting the missing or altered parts.

This approach allows BART to be effective in tasks that require generating or transforming text, such as summarization, translation, or text rewriting.\
BART 是一个编码器-解码器模型，类似于 **机器翻译** 系统中使用的架构。编码器处理输入序列，而解码器生成输出序列。BART 通过 **破坏输入数据**（如随机掩盖单词或句子），然后学习 **重构原始输入** 进行训练，类似于去噪自动编码器。

**编码器-解码器结构**

* **编码器**：编码器接收被破坏的输入（输入的部分被更改或移除），并处理它以捕捉有用的信息。
* **解码器**：解码器接收编码后的表示，通过预测缺失或更改的部分来重构原始文本。

这种方法使 BART 在需要生成或转换文本的任务中（如摘要、翻译或文本改写）非常有效。

#### 3. **Pre-training and Fine-tuning in BART | BART 的预训练和微调**

**Pre-training | 预训练**

BART is pre-trained using a variety of noise functions that corrupt the input data:

* **Text Infilling**: Random spans of text are masked and need to be predicted by the model. This teaches BART to reconstruct missing parts of a sequence, similar to how BERT works with masked tokens.
* **Sentence Permutation**: The order of sentences is shuffled, and BART is trained to reorder them correctly. This helps BART learn how to handle sentence-level relationships.

The combination of these tasks allows BART to capture both local context (like words within a sentence) and global context (like sentence order within a paragraph).\
BART 的预训练使用多种破坏输入数据的噪声函数：

* **文本填充**：随机掩盖文本中的部分内容，模型需要预测这些被掩盖的内容。这类似于 BERT 的掩蔽标记训练，教会 BART 如何重构序列的缺失部分。
* **句子置换**：打乱句子的顺序，并训练 BART 重新排序。这帮助 BART 学习句子级别的关系。

这些任务的结合使 BART 能够同时捕捉局部上下文（如句子中的词）和全局上下文（如段落中的句子顺序）。

**Fine-tuning | 微调**

After pre-training, BART is fine-tuned on task-specific datasets, such as for text summarization, machine translation, or question answering. During fine-tuning, the model's weights are adjusted to specialize in the task at hand, allowing BART to perform well on a wide range of tasks.\
预训练之后，BART 在任务特定的数据集上进行微调，如文本摘要、机器翻译或问答系统。在微调过程中，模型的权重会被调整以适应当前任务，使 BART 能够在各种任务中表现良好。

#### 4. **Key Features of BART | BART 的关键特性**

* **Denoising Autoencoder | 去噪自动编码器**: BART is trained to reconstruct corrupted text, making it effective at tasks that involve recovering or transforming text (e.g., summarization or translation). **去噪自动编码器**：BART 通过重构被破坏的文本进行训练，这使其在涉及恢复或转换文本的任务（如摘要或翻译）中表现出色。
* **Bidirectional and Autoregressive | 双向与自回归**: BART benefits from bidirectional context understanding (like BERT) and autoregressive text generation (like GPT), allowing it to handle both understanding and generation tasks effectively. **双向与自回归**：BART 结合了双向上下文理解（如 BERT）和自回归文本生成（如 GPT）的优势，使其能够有效处理理解和生成任务。
* **Flexible Architecture | 灵活架构**: BART's encoder-decoder structure makes it highly flexible and suitable for a variety of sequence-to-sequence tasks. **灵活架构**：BART 的编码器-解码器结构使其非常灵活，适用于多种序列到序列任务。

#### 5. **Applications of BART | BART 的应用**

* **Text Summarization | 文本摘要**: BART can generate concise summaries of long documents by focusing on key information and reducing text length. **文本摘要**：BART 能够通过关注关键信息并减少文本长度，生成长文档的简洁摘要。
* **Machine Translation | 机器翻译**: BART can be fine-tuned to translate text between different languages, offering high-quality translations. **机器翻译**：BART 可以通过微调执行不同语言之间的文本翻译，提供高质量的翻译。
* **Question Answering | 问答系统**: BART can be used to answer questions based on a given passage of text, making it useful in QA systems. **问答系统**：BART 可用于基于给定文本回答问题，使其在问答系统中非常有用。
* **Text Generation | 文本生成**: BART can be used to generate coherent and contextually appropriate text, similar to GPT models. **文本生成**：BART 可以生成连贯且上下文合适的文本，类似于 GPT 模型。

#### 6. **Advantages of BART | BART 的优势**

* **Versatility | 多功能性**: BART is effective for a variety of NLP tasks, including both text understanding and text generation, making it highly versatile. **多功能性**：BART 在多种 NLP 任务中表现出色，既包括文本理解任务也包括文本生成任务，使其非常多功能。
* **Effective Sequence-to-Sequence Model | 有效的序列到序列模型**: BART excels in sequence-to-sequence tasks, where both input and output are sequences, such as translation and summarization. **有效的序列到序列模型**：BART 在序列到序列任务（输入和输出都是序列）中表现突出，如翻译和摘要任务。
* **Combines Strengths of BERT and GPT | 结合 BERT 和 GPT 的优势**: By incorporating bidirectional context and autoregressive generation, BART brings together the strengths of both BERT (for understanding) and GPT (for generation). **结合 BERT 和 GPT 的优势**：通过结合双向上下文和自回归生成，BART 汇集了 BERT（理解任务）和 GPT（生成任务）的优势。

#### 7. **Limitations of BART | BART 的局限性**

* **Computationally Intensive | 计算密集**: Like most large Transformer-based models, BART requires significant computational resources, making it expensive to train and fine-tune. **计算密集**：与大多数基于 Transformer 的模型一样，BART 需要大量计算资源，训练和微调成本较高。
* **Slow Inference Speed | 推理速度较慢**: Due to its encoder-decoder architecture, BART may be slower at inference time compared to simpler models like GPT for generation tasks. **推理速度较慢**：由于其编码器-解码器架构，BART 在推理时可能比 GPT 等更简单的生成模型慢。





**BART** 是一个灵活的、编码器-解码器 Transformer 模型，在文本理解和生成任务中都表现出色。**关键特性**：结合了双向和自回归特性，作为去噪自动编码器进行训练，并且在序列到序列任务中非常有效。**应用**：文本摘要、机器翻译、问答系统和文本生成。**优势**：适用于多种 NLP 任务，有效的序列到序列模型，并结合了 BERT 和 GPT 的优势。**局限性**：计算密集，推理速度较慢。
