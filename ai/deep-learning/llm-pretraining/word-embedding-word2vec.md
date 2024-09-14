# Word Embedding(word2vec)

自然语言是用来表达人脑思维的复杂系统。在这个系统中，<mark style="color:blue;">词</mark>是意义的基本单元。

* 顾名思义，词向量是用于表示单词意义的向量
* 并且还可以被认为是单词的特征向量或表示

将单词映射到实向量的技术称为词嵌入（word2vec）



## 为何one-hot encoding是一个糟糕的选择

* 我们使用one-hot encoding来表示词（字符就是单词）。假设词典中不同词的数量（词典大小）为 $$N$$，每个词对应一个从 $$0$$ 到 $$N - 1$$ 的不同整数（索引）。
* 为了得到索引为 $$i$$ 的任意词的独热向量表示，我们创建了一个全为 $$0$$ 的长度为 $$N$$ 的向量，并将位置 (i) 的元素设置为 $$1$$。这样，每个词都被表示为一个长度为 $$N$$ 的向量，可以直接由神经网络使用。
* 虽然独热向量很容易构建，但它们通常不是一个好的选择。一个主要原因是独热向量不能准确表达不同词之间的相似度，比如我们经常使用的“余弦相似度”。对于向量 $$\mathbf{x}, \mathbf{y} \in \mathbb{R}^d$$，它们的余弦相似度是它们之间角度的余弦：

&#x20;                                                                                      $$\frac{\mathbf{x}^\top \mathbf{y}}{|\mathbf{x}| |\mathbf{y}|} \in [-1, 1]$$

* 由于任意两个不同词的独热向量之间的余弦相似度为 $$0$$，所以one-hot encoding不能编码词之间的相似性。

## 自监督的word2vec

* word2vec工具是为了解决上述问题而提出的。它将每个词映射到一个固定长度的向量，这些向量能更好地表达不同词之间的相似性和类比关系。
* word2vec工具包含两个模型，即跳元模型（skip-gram） (Mikolov et al., 2013)和连续词袋（CBOW） (Mikolov et al., 2013)。
* 对于在语义上有意义的表示，它们的训练依赖于条件概率，条件概率可以被看作使用语料库中一些词来预测另一些单词。由于是不带标签的数据，因此跳元模型和连续词袋都是自监督模型。

## 跳元模型（Skip-Gram）

* 跳元模型假设一个词可以用来在文本序列中生成其周围的单词。
* 以文本序列 "the""man""loves""his""son" 为例。
  * 假设中心词选择 "loves"，并将上下文窗口设置为 2，如图所示，给定中心词 "loves"，跳元模型考虑生成上下文词 "the""man""him""son" 的条件概率：$$P(\text{“the”, “man”, “his”, “son”} \mid \text{“loves”}).$$
  * 假设上下文词是在给定中心词的情况下独立生成的（即条件独立性）。在这种情况下，上述条件概率可以重写为：$$P(\text{“the”} \mid \text{“loves”}) \cdot P(\text{“man”} \mid \text{“loves”}) \cdot P(\text{“his”} \mid \text{“loves”}) \cdot P(\text{“son”} \mid \text{“loves”})$$
* 在跳元模型中，每个词都有两个 $$d$$ 维向量表示，用于计算条件概率。
  * 更具体地说，对于词典中索引为 $$i$$ 的任何词，分别用 $$\mathbf{v}_i \in \mathbb{R}^d$$ 和 $$\mathbf{u}_i \in \mathbb{R}^d$$ 表示其用作中心词和上下文词时的两个向量。
  * 给定中心词 $$w_c$$（词典中的索引为 $$c$$），生成任何上下文词 $$w_o$$（词典中的索引 $$o$$）的条件概率可以通过对向量点积的 softmax 操作来建模：$$P(w_o \mid w_c) = \frac{\exp(\mathbf{u}_o^\top \mathbf{v}c)}{\sum{i \in \mathcal{V}} \exp(\mathbf{u}_i^\top \mathbf{v}_c)},$$ 其中词表索引集 $$\mathcal{V} = {0, 1, \dots, |\mathcal{V}| - 1}$$。给定长度为 $$T$$ 的文本序列，其中时间步 $$t$$ 处的词表示为 \
    $$w^{(t)}$$。
* 假设上下文词是在给定任何中心词的情况下独立生成的。
  * 对于上下文窗口 $$m$$，跳元模型的似然函数是在给定任何中心词的情况下生成所有上下文词的概率：$$\prod_{t=1}^{T} \prod_{-m \leq j \leq m, j \neq 0} P(w^{(t+j)} \mid w^{(t)}),$$其中可以省略小于 1 或大于 $$T$$ 的任何时间步。



#### 跳元模型的训练

跳元模型参数是词表中每个词的中心词向量和上下文词向量。

* 在训练中，我们通过最大化似然函数（即极大似然估计）来学习模型参数。这相当于最小化以下损失函数：$$-\sum_{t=1}^{T} \sum_{-m \leq j \leq m, j \neq 0} \log P(w^{(t+j)} \mid w^{(t)}).$$
* 当使用随机梯度下降最小化损失时，在每次迭代中可以随机抽样一个较短的子序列来计算该子序列的（随机）梯度，以更新模型参数。
* 为了计算该（随机）梯度，我们需要获得对数条件概率关于中心词向量和上下文词向量的梯度。通常，涉及中心词 $$w_c$$ 和上下文词 $$w_o$$ 的对数条件概率为：$$\log P(w_o \mid w_c) = \mathbf{u}_o^\top \mathbf{v}c - \log \left( \sum{i \in \mathcal{V}} \exp(\mathbf{u}_i^\top \mathbf{v}_c) \right).$$
* 通过微分，我们可以获得其相对于中心词向量 $$\mathbf{v}_c$$ 的梯度为：
* $$\frac{\partial \log P(w_o \mid w_c)}{\partial \mathbf{v}_c} = \mathbf{u}o - \frac{\sum{j \in \mathcal{V}} \exp(\mathbf{u}_j^\top \mathbf{v}_c) \mathbf{u}j}{\sum{i \in \mathcal{V}} \exp(\mathbf{u}_i^\top \mathbf{v}_c)}$$$$= \mathbf{u}o - \sum{j \in \mathcal{V}} P(w_j \mid w_c) \mathbf{u}_j.$$
* 注意，计算需要词典中以 $$w_c$$ 为中心词的所有词的条件概率。其他词向量的梯度可以以相同的方式获得。
* 对词典中索引为 $$i$$ 的词进行训练后，得到 $$\mathbf{v}_i$$（作为中心词）和 $$\mathbf{u}_i$$（作为上下文词）两个向量。在自然语言处理应用中，跳元模型的中心词向量通常用于词向量表示。



## 连续词袋(CBOW)模型

连续词袋（CBOW）模型类似于跳元模型。与跳元模型的主要区别在于，连续词袋模型假设<mark style="color:purple;">中心词是基于其在文本序列中的周围上下文词生成的</mark>。

* 例如，在文本序列 “the”“man”“loves”“his”“son” 中，在 “loves” 为中心词且上下文窗口为2的情况下，连续词袋模型考虑基于上下文词 “the”“man”“him”“son” 生成中心词 “loves” 的条件概率，即：$$P(\text{“loves”} \mid \text{“the”, “man”, “his”, “son”}).$$

由于连续词袋模型中存在多个上下文词，因此在计算条件概率时对这些上下文词向量进行平均。

* 具体地说，对于字典中索引为 (i) 的任意词，分别用 $$\mathbf{v}_i \in \mathbb{R}^d$$ 和  $$\mathbf{u}_i \in \mathbb{R}^d$$表示用作上下文词和中心词的两个向量（符号与跳元模型中相反）。给定上下文词 $$w{o_1}, \ldots, w{o_{2m}}$$（在词表中索引是 $$o_1, \ldots, o_{2m})$$，生成任意中心词 $$w_c$$（在词表中索引是 $$c$$）的条件概率可以由以下公式建模：$$P(w_c \mid w_{o_1}, \ldots, w_{o_{2m}}) = \frac{\exp\left( \frac{1}{2m} \mathbf{u}c^\top (\mathbf{v}{o_1} + \ldots + \mathbf{v}{o{2m}}) \right)}{\sum_{i \in \mathcal{V}} \exp\left( \frac{1}{2m} \mathbf{u}i^\top (\mathbf{v}{o_1} + \ldots + \mathbf{v}{o{2m}}) \right)}.$$
* 为了简洁起见，我们设为 $$\mathbf{W}o = {w_{o_1}, \ldots, w_{o_{2m}}}$$ 和 $$\bar{\mathbf{v}}o = (\mathbf{v}{o_1} + \ldots + \mathbf{v}{o{2m}})/(2m)$$。那么这个式子可以简化为：$$P(w_c \mid \mathbf{W}_o) = \frac{\exp(\mathbf{u}_c^\top \bar{\mathbf{v}}o)}{\sum{i \in \mathcal{V}} \exp(\mathbf{u}_i^\top \bar{\mathbf{v}}_o)}.$$ 给定长度为 (T) 的文本序列，其中时间步 (t) 处的词表示为 (w^{(t)})。对于上下文窗口 (m)，连续词袋模型的似然函数是在给定其上下文词的情况下生成所有中心词的概率：$$\prod_{t=1}^{T} P(w^{(t)} \mid w^{(t-m)}, \ldots, w^{(t-1)}, w^{(t+1)}, \ldots, w^{(t+m)}).$$



#### CBOW的训练

训练连续词袋模型与训练跳元模型几乎是一样的。连续词袋模型的最大似然估计等价于最小化以下损失函数：

$$\sum_{t=1}^{T} \log P(w^{(t)} \mid w^{(t-m)}, \ldots, w^{(t-1)}, w^{(t+1)}, \ldots, w^{(t+m)}).$$

请注意，$$\log P(w_c \mid \mathbf{W}_o) = \mathbf{u}_c^\top \bar{\mathbf{v}}o - \log \left( \sum{i \in \mathcal{V}} \exp (\mathbf{u}_i^\top \bar{\mathbf{v}}_o) \right).$$

通过微分，我们可以获得其关于任意上下文词向量 (\mathbf{v}\_{o\_i})（(i = 1, \ldots, 2m)）的梯度，如下：$$\frac{\partial \log P(w_c \mid \mathbf{W}o)}{\partial \mathbf{v}{o_i}} = \frac{1}{2m} \left( \mathbf{u}c - \frac{\sum{j \in \mathcal{V}} \exp (\mathbf{u}_j^\top \bar{\mathbf{v}}_o) \mathbf{u}j}{\sum{i \in \mathcal{V}} \exp (\mathbf{u}_i^\top \bar{\mathbf{v}}_o)} \right) = \frac{1}{2m} \left( \mathbf{u}c - \sum{j \in \mathcal{V}} P(w_j \mid \mathbf{W}_o) \mathbf{u}_j \right).$$

其他词向量的梯度可以以相同的方式获得。

与跳元模型不同，连续词袋模型通常使用上下文词向量作为词表示。



