# Bidirectional Encoder Representations from Transformers(BERT)





Bert:

类型

* Bert中双向上下文信息的广义自回归模型XLNtet
* 也有改进BERT训练方式和目标的RoBERTa和SpanBERt
* 还有结合多任务以及知识蒸馏（Knowledge Distillation）强化BERT的MT-DNN

关键：

* 引入pre-trained 模型， constructed by Transformer
* use autoencoder：引入噪声数据重建原始数据
* pre-trained：variational autoencoder/mask language model（not autogressive model）
  * benefit：bidirectional info
  * problem：
    * Pretrain-finetune Discrepancy（预处理的时候\[mask]在微调（fine-tuning）时并不会出现，使得两个过程不一致，不利于learning）
    * Independence assumption：each token prediction is independent，如果new york这样的entity存在关系，但是这个假设忽略这个情景
  *

XLNet：

* Permutation Language Model：使用输入的 permutation 获取双向的上下文信息，同时维持自回归模型原有的单向形式。这样的好处是可以不用改变输入顺序，只需在内部处理。
  * 使用 token 在 permutation 的位置计算上下文信息。如对于，当前有一个 2 -> 4 ->3 ->1 的排列，那么我们就取出 token\_2 和 token\_4 作为AR 的输入预测 token\_3。不难理解，当所有 permutation 取完时，我们就能获得所有的上下文信息。
  * 但是在原来的公式中，我们只使用了 h\_θ (x\_(Z\<t)) 来表示当前token“上文”的 hidden representation，使得不管模型要预测哪个位置的 token，如果“上文”一致，那么输出就是一致的。因此，新的公式做出了改变，引入了要预测的 token 的位置信息。
  * 此外，为了降低模型的优化难度，XLNet 使用了 Partial Prediction，即只预测当前 permutation 位置 c 之后的 token，最终优化目标如下所示。
* Two-Stream Self Attention
  * 该机制所要解决的问题是，当我们获得了 g\_θ (x\_{Z\<t},z\_t) 后，我们只有该位置信息以及“上文”的信息，不足以去预测该位置后的 token；而原来的 h\_θ (x\_{Z\<t}) 则因为获取不到位置信息，依然不足以去预测。因此，XLNet 引入了 Two-Stream Self-Attention 机制，将两者结合起来
* Recurrence Mechanism
  * 该机制来自 Transformer-XL，即在处理下一个 segment 时结合上个 segment 的 hidden representation，使得模型能够获得更长距离的上下文信息。而在 XLNet 中，虽然在前端采用相对位置编码，但在表示 h\_θ (x\_{Z\<t}) 的时候，涉及到的处理与permutation 独立，因此还可以沿用这个机制。该机制使得 XLNet 在处理长文档时具有较好的优势。

### Transformer

Autocoder什么意思？

* 相当于你从deep learning模型用到nlp问题上所需要的第一部分转化工作，当作feature engineering？后面再谈bert，tranformer模型，因为这两个是特别针对文本问题？
  * rnn是一个个单词输入，这个是一句话，这样就有前后关系
  * transformer优势1:不管当前词和其他词的空间距离有多远，包含其他词的信息不取决于距离，而是取决于两者的相关性，这是Transformer的第一个优势。
  * transformer优势2:对于Transformer来说，在对当前词进行计算的时候，不仅可以用到前面的词，也可以用到后面的词。
  * transformer优势3:可能有人会不认可，RNN的结构包含了序列的时序信息，而Transformer却完全把时序信息给丢掉了。为了解决时序的问题，Transformer的作者用了一个绝妙的办法，这就是在前文提到的位置编码（Positional Encoding）
* 第一部分word embedding：
  * word 2 vec 把文字转化成vector feature（query，key，value）
* 第二部分Multi-Head Attention：
  * 计算score/归一化/softmax来算出probability，当作词典？
  * 这就是attention的含义，让其不在孤立，输出跟哪个词关联比较强，就放比较多的注意力在上面。
  * 而这个若干组就是multi-head的head数，一是多个组可以并行计算，二是不同的组可以捕获不同的子空间的信息。
* 然后经过一个归一化normalization的操作。接着经过一个两层的全连接网络，最后同样是shortcut和normalization的操作

BERT

* 我们把Transformer encoder的结构作为一个基本单元，把N个这样的基本单元顺序连起来，就是BERT的算法模型
* BERT是怎么训练的呢？BERT来自于Bidirectional Encoder Representations from Transformers首字母缩写，这里提到了一个双向（Bidirectional）的概念。
  * BERT在一个33亿单词的语料库上做预训练，预训练包括两个任务，第一个任务是随机的扣掉15%的单词（为什么是15%作者没说，很tricky），用一个掩码MASK代替，让模型去预测这个单词；第二个任务是每个训练样本是一个上下句，有50%的样本，下句和上句是真实的，另外50%的样本，下句和上句是无关的，模型需要判断两句的关系。这两个任务各有一个loss，将这两个loss加起来作为总的loss进行优化。
  * 以看到，相比于GPT，BERT是预测文中扣掉的词，可以充分利用到上下文的信息，这使得模型有更强的表达能力，这也是BERT中Bidirectional的含义。在一些NLP任务中需要判断句子关系，比如判断两句话是否有相同的含义。BERT有了第二个任务，就能够很好的捕捉句子之间的关系。
* 图3.2表示“my dog is cute, he likes playing.”的输入形式。每个符号的输入由三个部分构成，一个是词本身的embedding；第二个是表示上下句的embedding，如果是上句，就用A embedding，如果是下句，就用B embedding；最后，根据Transformer模型的特点，还要加上位置embedding，这里的位置embedding是通过学习的方式得到的，BERT设计一个样本最多支持512个位置；将3个embedding相加，作为输入。需要注意的是，在每个句子的开头，需要加一个Classification（CLS）符号，后文中会进行介绍，其他细节省略。
* 词语本身embedding，词语位置上的embedding（CLS）
