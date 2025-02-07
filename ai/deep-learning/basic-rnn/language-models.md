# Language Models

* &#x20;我们了解了如何将文本数据映射为词元， 以及将这些词元可以视为一系列离散的观测，例如单词或字符。 假设长度为$$T$$的文本序列中的词元依次为$$x_1,x_2, \cdots, x_T$$。 于是，$$x_t$$（$$1 \leq t \leq T$$） 可以被认为是文本序列在时间步$$t$$处的观测或标签。 在给定这样的文本序列时，_语言模型_（language model）的目标是估计序列的联合概率$$P(x_1, \cdots, x_T)$$
* 例如，只需要一次抽取一个词元$$x_t \sim P(x_t|x_{t-1},\cdots, x_1)$$， 一个理想的语言模型就能够基于模型本身生成自然文本。 与猴子使用打字机完全不同的是，从这样的模型中提取的文本 都将作为自然语言（例如，英语文本）来传递。 只需要基于前面的对话片断中的文本， 就足以生成一个有意义的对话。

### Learning Language Models

Suppose that we tokenize text data at the word level. Let’s start by applying basic probability rules:

$$P(x_1, x_2, \cdots, x_T) = \Pi_{t= 1}^{T} P(x_t |x_1, \cdots, x_{t-1})$$

For example, the probability of a text sequence containing four words would be given as:

$$P(deep, learning, is, fun) = P(deep)P(learning | deep) P(is| deep, learning) P(fun | deep, learning, is)$$

#### Markov Models and N-grams

* 在讨论包含深度学习的解决方案之前，我们需要了解更多的概念和术语。 回想一下我们在 [8.1节](https://zh.d2l.ai/chapter_recurrent-neural-networks/sequence.html#sec-sequence)中对马尔可夫模型的讨论， 并且将其应用于语言建模。 如果$$P(x_{t+1} | x_{t} , \cdots, x_1) = P(x_{t+1}|x_t)$$， 则序列上的分布满足一阶马尔可夫性质。 阶数越高，对应的依赖关系就越长。 这种性质推导出了许多可以应用于序列建模的近似公式
* 通常，涉及一个、两个和三个变量的概率公式分别被称为 _一元语法_（unigram）、_二元语法_（bigram）&#x548C;_&#x4E09;元语法_（trigram）模型。 下面，我们将学习如何去设计更好的模型。

#### Word Frequency

* The probability of words can be calculated from the relative word frequency of a given word in the training dataset.

#### Laplace Smoothing

* A common strategy is to perform some form of _Laplace smoothing_. The solution is to add a small constant to all counts. Denote by $$n$$ the total number of words in the training set and $$m$$ the number of unique words. This solution helps with singletons.

### Perplexity(困惑度)

We defined entropy, surprisal, and cross-entropy混乱程度来考虑问题

### Partitioning Sequences(总共的长度)

* 当序列变得太长而不能被模型一次性全部处理时， 我们可能希望拆分这样的序列方便模型读取。
* 在介绍该模型之前，我们看一下总体策略。 假设我们将使用神经网络来训练语言模型， 模型中的网络一次处理具有预定义长度 （例如$$n$$个时间步）的一个小批量序列。 现在的问题是如何随机生成一个小批量数据的特征和标签以供读取。
*

    <figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 at 5.17.16 PM.png" alt="" width="375"><figcaption></figcaption></figure>
* &#x20;事实上，他们都一样的好。 然而，如果我们只选择一个偏移量， 那么用于训练网络的、所有可能的子序列的覆盖范围将是有限的。 因此，我们可以从随机偏移量开始划分序列， 以同时获&#x5F97;_&#x8986;盖性_（coverage）&#x548C;_&#x968F;机性_（randomness）
* 下面，我们将描述如何实&#x73B0;_&#x968F;机采样_（random sampling）和 _顺序分区_（sequential partitioning）策略。

#### random sampling

* 在随机采样中，每个样本都是在原始的长序列上任意捕获的子序列。 在迭代过程中，来自两个相邻的、随机的、小批量中的子序列不一定在原始序列上相邻。 对于语言建模，目标是基于到目前为止我们看到的词元来预测下一个词元， 因此标签是移位了一个词元的原始序列。
* 下面的代码每次可以从数据中随机生成一个小批量。 在这里，参数`batch_size`指定了每个小批量中子序列样本的数目， 参数`num_steps`是每个子序列中预定义的时间步数。

#### sequential partitioning

* 在迭代过程中，除了对原始序列可以随机抽样外， 我们还可以保证两个相邻的小批量中的子序列在原始序列上也是相邻的。 这种策略在基于小批量的迭代过程中保留了拆分的子序列的顺序，因此称为顺序分区。
