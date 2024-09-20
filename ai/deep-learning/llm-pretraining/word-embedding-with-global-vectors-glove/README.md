# Word Embedding with Global Vectors(GloVe)

### Word Embedding with Global Vectors (GloVe) | 全局向量词嵌入 (GloVe)

#### 1. **What is GloVe? | 什么是 GloVe？**

**GloVe (Global Vectors for Word Representation)** is a word embedding technique developed by researchers at Stanford in 2014. Like **word2vec**, GloVe represents words as dense vectors in a continuous vector space, where semantically similar words are closer to each other. However, GloVe differs in its approach to learning word embeddings. While word2vec is based on predicting words in a local context using neural networks, GloVe uses **global co-occurrence statistics** to capture relationships between words across the entire text corpus.

In GloVe, the idea is to learn word embeddings based on how frequently words co-occur in a given corpus. The result is a set of word vectors that capture both local context and global statistical information about word relationships.\
**GloVe（全局向量词表示）** 是斯坦福大学研究人员在 2014 年开发的一种词嵌入技术。与 **word2vec** 类似，GloVe 将单词表示为连续向量空间中的稠密向量，其中语义相似的单词彼此靠近。然而，GloVe 在学习词嵌入的方法上有所不同。word2vec 基于使用神经网络预测局部上下文中的单词，而 GloVe 使用 **全局共现统计** 捕捉整个语料库中单词之间的关系。

在 GloVe 中，基本思想是基于单词在给定语料库中共同出现的频率学习词嵌入。结果是一组既捕捉局部上下文又包含全局统计信息的词向量。

#### 2. **How Does GloVe Work? | GloVe 是如何工作的？**

GloVe uses **co-occurrence matrices** to learn word embeddings. The matrix records how often pairs of words occur together in a large corpus. The intuition behind GloVe is that words that appear in similar contexts should have similar vector representations.

**Co-Occurrence Matrix | 共现矩阵**

A **co-occurrence matrix** is built, where each element in the matrix represents how often a word appears in the context of another word within a given window size (e.g., 5 or 10 words). For example, in the sentence "The cat sat on the mat," the words "cat" and "sat" might co-occur frequently in many contexts.

**GloVe Objective Function | GloVe 目标函数**

GloVe learns word embeddings by minimizing the difference between the actual co-occurrence count and the predicted count from the word vectors. The objective function is designed to ensure that the ratio of co-occurrence probabilities between words is captured in the word vectors:

$$
J = \sum_{i,j=1}^{V} f(X_{ij}) \left( w_i^T \cdot w_j + b_i + b_j - \log(X_{ij}) \right)^2
$$

Where:

* $$X_{ij}$$ is the number of times word $$i$$ and word $$j$$ co-occur,
* $$w_i$$ and $$w_j$$ are the word vectors for words $$i$$ and $$j$$,
* $$b_i$$ and $$b_j$$ are bias terms for words $$i$$ and $$j$$,
* $$f(X_{ij})$$ is a weighting function to control the impact of frequent and rare words.

The goal is to learn word vectors $$w_i$$ such that they accurately capture the statistical co-occurrence relationships between words.\
GloVe 使用 **共现矩阵** 来学习词嵌入。矩阵记录了单词对在大语料库中一起出现的频率。GloVe 背后的直觉是，出现在相似上下文中的单词应该具有相似的向量表示。

**共现矩阵**

构建一个 **共现矩阵**，矩阵中的每个元素表示一个单词在另一个单词的上下文中出现的频率，窗口大小为预定值（例如 5 或 10 个单词）。例如，在句子 “The cat sat on the mat”（猫坐在垫子上）中，单词 “cat” 和 “sat” 可能在许多上下文中频繁共现。

**GloVe 目标函数**

GloVe 通过最小化实际共现次数与从词向量预测的共现次数之间的差异来学习词嵌入。目标函数设计为确保单词之间的共现概率比在词向量中得到准确表示：

$$
J = \sum_{i,j=1}^{V} f(X_{ij}) \left( w_i^T \cdot w_j + b_i + b_j - \log(X_{ij}) \right)^2
$$

其中：

* $$X_{ij}$$ 是单词 $$i$$ 和单词 $$j$$ 的共现次数，
* $$w_i$$ 和 $$w_j$$ 是单词 $$i$$ 和 $$j$$ 的词向量，
* $$b_i$$ 和 $$b_j$$ 是单词 $$i$$ 和 $$j$$ 的偏置项，
* $$f(X_{ij})$$ 是控制频繁和稀有单词影响的加权函数。

目标是学习词向量 $$w_i$$，使其准确捕捉单词之间的统计共现关系。

#### 3. **Key Features of GloVe | GloVe 的关键特性**

* **Global Co-Occurrence Statistics | 全局共现统计**: GloVe uses information from the entire corpus to learn word embeddings, capturing global statistical relationships between words. **全局共现统计**：GloVe 使用整个语料库中的信息来学习词嵌入，捕捉单词之间的全局统计关系。
* **Efficiency | 高效性**: GloVe uses a matrix factorization approach, which is more computationally efficient for large datasets compared to methods that rely on sliding context windows. **高效性**：GloVe 使用矩阵分解方法，与依赖滑动窗口的其他方法相比，对于大数据集的计算效率更高。
* **Logarithmic Scaling | 对数缩放**: The use of logarithmic scaling in the objective function helps GloVe better handle the wide range of co-occurrence counts, from very frequent to very rare word pairs. **对数缩放**：目标函数中使用对数缩放帮助 GloVe 更好地处理从非常频繁到非常稀有的单词对的共现次数。

#### 4. **Benefits of GloVe | GloVe 的优势**

* **Captures Semantic Relationships | 捕捉语义关系**: GloVe effectively captures semantic relationships between words, such as word analogies (e.g., "king" is to "queen" as "man" is to "woman"). **捕捉语义关系**：GloVe 有效地捕捉单词之间的语义关系，例如词类比（如 "king" 之于 "queen" 正如 "man" 之于 "woman"）。
* **Better Global Understanding | 更好的全局理解**: Unlike word2vec, which focuses on local context, GloVe incorporates global co-occurrence statistics, leading to embeddings that better capture overall word relationships in the corpus. **更好的全局理解**：与专注于局部上下文的 word2vec 不同，GloVe 融入了全局共现统计，生成的词嵌入更好地捕捉了语料库中的整体单词关系。
* **Handling Rare Words | 处理稀有单词**: By using global co-occurrence data, GloVe is better at handling rare words compared to models like word2vec, which may struggle when certain words appear infrequently in the local context. **处理稀有单词**：通过使用全局共现数据，GloVe 在处理稀有单词方面表现得更好，相比之下，像 word2vec 这样的模型可能在某些单词在局部上下文中出现频率较低时表现不佳。

#### 5. **Limitations of GloVe | GloVe 的局限性**

* **Context Independence | 上下文独立性**: Like word2vec, GloVe assigns a single vector to each word, meaning it cannot capture different meanings of the same word in different contexts (polysemy). **上下文独立性**：与 word2vec 类似，GloVe 为每个单词分配一个固定的向量，这意味着它无法捕捉同一个单词在不同上下文中的不同含义（多义性）。
* **Requires Large Datasets | 需要大规模数据集**: GloVe requires large corpora to accurately capture co-occurrence statistics. Small datasets may not provide enough co-occurrence information for the model to learn meaningful word embeddings. **需要大规模数据集**：GloVe 需要大型语料库来准确捕捉共现统计数据。小数据集可能无法提供足够的共现信息来让模型学习到有意义的词嵌入。

#### 6. **Applications of GloVe | GloVe 的应用**

* **Word Similarity and Analogy Tasks | 词语相似性和类比任务**: GloVe embeddings are commonly used for tasks like identifying similar words or solving word analogy problems (e.g., "man" is to "king" as "woman" is to "queen"). **词语相似性和类比任务**：GloVe 嵌入常用于识别相似词或解决词类比问题（如 "man" 之于 "king" 正如 "woman" 之于 "queen"）。
* **Text Classification | 文本分类**: GloVe vectors can serve as input features for text classification models, helping the model to better understand the semantic content of text data. **文本分类**：GloVe 向量可以作为文本分类模型的输入特征，帮助模型更好地理解文本数据的语义内容。
* **Sentiment Analysis | 情感分析**: GloVe is used in sentiment analysis tasks to analyze the sentiment of a text by leveraging the learned word embeddings that capture the nuances of positive or negative sentiment. **情感分析**：GloVe 用于情感分析任务，通过利用学习到的词嵌入来分析文本的情感，这些词嵌入能够捕捉到正面或负面情感的细微差别。
* **Machine Translation | 机器翻译**: GloVe embeddings can be used to align words across languages in machine translation tasks, aiding in the translation process by capturing the relationships between words in different languages. **机器翻译**：GloVe 嵌入可以用于机器翻译任务中的跨语言单词对齐，通过捕捉不同语言中单词之间的关系来帮助翻译过程。



**GloVe** 是一种通过使用整个语料库的全局共现统计来捕捉单词关系的词嵌入模型。**工作原理**：它构建共现矩阵，并通过最小化实际和预测共现次数之间的差异来学习词嵌入。**优势**：捕捉语义关系，融入全局统计，能够很好地处理稀有单词。**局限性**：为每个单词分配一个向量，无法捕捉多义性，并且需要大规模数据集。**应用**：词语相似性、文本分类、情感分析和机器翻译等。
