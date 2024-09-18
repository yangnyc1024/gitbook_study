# Basic Raw Text to Seq

Typical preprocessing pipelines execute the following steps:

1. Load text as strings into memory. (text--> string)
2. Split the strings into tokens (e.g., words or characters). (string --> token)
3. Build a vocabulary dictionary to associate each vocabulary element with a numerical index. (vocabulary dict)
4. Convert the text into sequences of numerical indices. (dict --> numerical indices)



### Reading the Dataset

* just read..... or might you need to ignore punctuation and capitalization when preprocessing the raw text



### Tokenization

* _Tokens_ are the atomic (indivisible) units of text. Each time step corresponds to 1 token, but what precisely constitutes a token is a design choice.(token是最小的元素)
* Sometimes, we tokenize our preprocessed text into a sequence of characters.



### Vocabulary

* _vocabularies_, i.e., objects that associate each distinct token value with a unique index
* &#x20;我们先将训练集中的所有文档合并在一起，对它们的唯一词元进行统计， 得到的统计结果称之为_语料_（corpus）。 然后根据每个唯一词元的出现频率，为其分配一个数字索引。
* 很少出现的词元通常被移除，这可以降低复杂性。 另外，语料库中不存在或已删除的任何词元都将映射到一个特定的未知词元“\<unk>”。 我们可以选择增加一个列表，用于保存那些被保留的词元， 例如：填充词元（“\<pad>”）； 序列开始词元（“\<bos>”）； 序列结束词元（“\<eos>”）。



#### Wrap Up

* 在使用上述函数时，我们将所有功能打包到`load_corpus_time_machine`函数中， 该函数返回`corpus`（词元索引列表）和`vocab`（时光机器语料库的词表）。 我们在这里所做的改变是：
  1. 为了简化后面章节中的训练，我们使用字符（而不是单词）实现文本词元化；
  2. 时光机器数据集中的每个文本行不一定是一个句子或一个段落，还可能是一个单词，因此返回的`corpus`仅处理为单个列表，而不是使用多词元列表构成的一个列表。

\




