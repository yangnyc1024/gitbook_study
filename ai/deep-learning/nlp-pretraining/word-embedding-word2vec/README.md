# Word Embedding(word2vec)

### Word Embedding (word2vec) | 词嵌入 (word2vec)

#### 1. **What is Word Embedding? | 什么是词嵌入？**

**Word Embedding** is a technique used in natural language processing (NLP) to represent words as continuous vectors in a fixed-dimensional space. Instead of using sparse representations like one-hot encoding, word embeddings capture semantic meaning by placing words with similar meanings closer together in the vector space. This enables machine learning models to understand relationships between words, such as **synonyms**, **analogies**, and **contextual meanings**.

**word2vec** is a popular word embedding model developed by Google in 2013. It uses neural networks to learn word representations from large text corpora and maps each word to a dense vector where similar words are placed close to each other.\
**词嵌入** 是自然语言处理 (NLP) 中的一种技术，用于将单词表示为固定维度空间中的连续向量。与稀疏表示（如 one-hot 编码）不同，词嵌入通过将具有相似含义的单词在向量空间中靠近来捕捉语义。这使得机器学习模型能够理解单词之间的关系，如 **同义词**、**类比** 和 **上下文含义**。

**word2vec** 是谷歌在 2013 年开发的一种流行的词嵌入模型。它使用神经网络从大量文本语料库中学习单词表示，并将每个单词映射到一个稠密向量，其中相似的单词彼此靠近。

#### 2. **How Does word2vec Work? | word2vec 是如何工作的？**

word2vec operates in two main ways to learn word embeddings:

1. **Skip-Gram Model**: The model predicts the **context words** (surrounding words) given a **target word**. For example, given the target word "dog," the model predicts words like "bark," "pet," and "animal."
2. **Continuous Bag of Words (CBOW)**: The model predicts the **target word** given the surrounding **context words**. For instance, if the context is "The dog \_\_\_\_ loudly," the model predicts the target word "barks."

Both methods rely on the assumption that words appearing in similar contexts are likely to have similar meanings, and they use neural networks to learn the weights (word vectors) that capture these relationships.\
word2vec 有两种主要方法学习词嵌入：

1. **Skip-Gram 模型**：该模型在给定 **目标词** 的情况下预测 **上下文词**（周围的单词）。例如，给定目标词 “dog”（狗），模型预测像 “bark”（吠）、“pet”（宠物）和 “animal”（动物）这样的单词。
2. **连续词袋 (CBOW)**：该模型在给定周围 **上下文词** 的情况下预测 **目标词**。例如，如果上下文是 “The dog \_\_\_\_ loudly”（这只狗大声地\_\_\_\_），模型预测目标词 “barks”（吠）。

这两种方法都依赖于一个假设，即出现在相似上下文中的单词很可能具有相似的含义，它们通过神经网络学习捕捉这些关系的权重（词向量）。

#### 3. **Skip-Gram Model | Skip-Gram 模型**

The **Skip-Gram** model takes a target word as input and tries to predict the surrounding context words. It maximizes the probability of context words appearing close to the target word. The goal is to learn word vectors such that words appearing in similar contexts have similar vector representations.

For example, for the sentence "The dog barked loudly," the target word might be "dog," and the context words could be "The," "barked," and "loudly." The model tries to predict these context words based on the target word.\
**Skip-Gram** 模型以目标词为输入，试图预测周围的上下文词。它最大化上下文词出现在目标词附近的概率。目标是学习词向量，使得出现在相似上下文中的单词具有相似的向量表示。

例如，对于句子 “The dog barked loudly”（这只狗大声地吠），目标词可能是 “dog”（狗），而上下文词可能是 “The”（这只）、“barked”（吠）和 “loudly”（大声）。模型根据目标词预测这些上下文词。

The objective function for Skip-Gram is to maximize the likelihood of predicting the context words:

$$
\text{maximize } \sum_{t=1}^{T} \sum_{-m \leq j \leq m, j \neq 0} \log P(w_{t+j} | w_t)
$$

Where:

* $$w_t$$ is the target word,
* $$w_{t+j}$$ is the context word within a window of size $$m$$.

Skip-Gram 的目标函数是最大化预测上下文词的可能性：

$$
\text{maximize } \sum_{t=1}^{T} \sum_{-m \leq j \leq m, j \neq 0} \log P(w_{t+j} | w_t)
$$

其中：

* $$w_t$$ 是目标词，
* $$w_{t+j}$$ 是窗口大小为 $$m$$ 的上下文词。

#### 4. **Continuous Bag of Words (CBOW) | 连续词袋模型 (CBOW)**

The **CBOW** model works in the opposite direction of Skip-Gram. Given a set of context words, it predicts the target word. For example, for the sentence "The dog barked loudly," if the context words are "The," "barked," and "loudly," the CBOW model predicts "dog."

The objective function for CBOW is to maximize the likelihood of predicting the target word:

$$
\text{maximize } \sum_{t=1}^{T} \log P(w_t | w_{t-m}, \dots, w_{t-1}, w_{t+1}, \dots, w_{t+m})
$$

Both Skip-Gram and CBOW are trained using a neural network, and the weights of the network are the learned word embeddings.\
**CBOW** 模型与 Skip-Gram 相反。给定一组上下文词，它预测目标词。例如，对于句子 “The dog barked loudly”，如果上下文词是 “The”、 “barked” 和 “loudly”，CBOW 模型预测 “dog”。

CBOW 的目标函数是最大化预测目标词的可能性：

$$
\text{maximize } \sum_{t=1}^{T} \log P(w_t | w_{t-m}, \dots, w_{t-1}, w_{t+1}, \dots, w_{t+m})
$$

Skip-Gram 和 CBOW 都通过神经网络进行训练，网络的权重即为学习到的词嵌入。

#### 5. **Benefits of word2vec | word2vec 的优势**

* **Captures Semantic Relationships | 捕捉语义关系**: word2vec can capture meaningful relationships between words, such as **king** - **man** + **woman** = **queen**, allowing it to understand analogies and word similarities. **捕捉语义关系**：word2vec 能够捕捉单词之间的有意义的关系，例如 **国王** - **男人** + **女人** = **女王**，这使其能够理解类比和词语相似性。
* **Dense and Low-Dimensional Vectors | 稠密低维向量**: word2vec represents words in dense vectors (e.g., 100 to 300 dimensions), making it more efficient and informative than sparse representations like one-hot encoding. **稠密低维向量**：word2vec 用稠密向量表示单词（如 100 到 300 维），使其比稀疏表示（如 one-hot 编码）更高效且信息量更大。
* **Context-Based Representation | 基于上下文的表示**: word2vec uses the context in which a word appears to learn its meaning, making it sensitive to the nuances in word usage. **基于上下文的表示**：word2vec 使用单词出现的上下文来学习其含义，使其能够对单词用法中的细微差别敏感。

#### 6. **Limitations of word2vec | word2vec 的局限性**

* **Word-Level Representation | 基于单词的表示**: word2vec provides a single vector for each word, regardless of its meaning in different contexts (polysemy), so it cannot capture the various meanings of a word based on its context. **基于单词的表示**：word2vec 为每个单词提供一个固定的向量，不考虑其在不同上下文中的含义（多义性），因此它无法根据上下文捕捉单词的多种含义。
* **Requires Large Datasets | 需要大规模数据集**: word2vec requires large amounts of text data to learn good-quality word embeddings. If trained on small datasets, the embeddings may not capture the true relationships between words. **需要大规模数据集**：word2vec 需要大量文本数据来学习高质量的词嵌入。如果在小数据集上训练，词嵌入可能无法捕捉单词之间的真实关系。

#### 7. **Applications of word2vec | word2vec 的应用**

* **Word Similarity and Analogy Tasks | 词语相似性和类比任务**: word2vec is commonly used to find similar words or solve word analogy tasks. For example, finding that **Paris** is to **France** as **Tokyo** is to **Japan**. **词语相似性和类比任务**：word2vec 常用于寻找相似单词或解决单词类比任务。例如，找到 “Paris”（巴黎）之于 “France”（法国）正如 “Tokyo”（东京）之于 “Japan”（日本）。
* **Text Classification and Sentiment Analysis | 文本分类和情感分析**: word2vec embeddings can be used as features for text classification or sentiment analysis tasks, where the learned embeddings help the model understand the meaning of words. **文本分类和情感分析**：word2vec 嵌入可以作为文本分类或情感分析任务的特征，学习到的嵌入帮助模型理解单词的含义。
* **Machine Translation | 机器翻译**: word2vec embeddings can be used to align words in different languages, making it useful for machine translation tasks where words with similar meanings need to be aligned across languages. **机器翻译**：word2vec 嵌入可用于对齐不同语言中的单词，这在机器翻译任务中非常有用，因为具有相似含义的单词需要在不同语言之间对齐。



**word2vec** 是一种流行的词嵌入模型，通过将单词表示为稠密向量来捕捉它们之间的语义关系。**模型**：Skip-Gram 基于目标词预测上下文词，而 CBOW 基于上下文词预测目标词。**优势**：捕捉词语相似性，使用稠密低维向量，学习基于上下文的单词含义。**局限性**：无法处理多义性（多重含义），需要大规模数据集。**应用**：词语相似性任务、文本分类、情感分析和机器翻译等。



##



