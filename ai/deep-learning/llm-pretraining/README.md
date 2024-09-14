# LLM Pretraining

人与人之间的交流，是由语言来承载信息的，尤其是在这信息大爆炸的时代。如何让计算机可以更好理解人的语言，以至于可以帮助做决策成为了一个很重要的研究方向。

我们会在之后的部分中，学习到

* 当将每个单词或者子词视为单个词元，可以先在大型语料库上使用word2vec，GloVe，子词嵌入模型预先训练，这些每个词元的词元
* 当经过预训练后，每个词元的表示可以是一个向量，但是上下文发生改变，它都会保持不变
* example：go to the bank to deposit some money（去银行存点钱） vs go to the bank to sit down”（去河岸坐下来）上下文中是相同的。
* 因此许多新的预训练模型使用相同的词元的表示适用与不同的上下文，其中包括了<mark style="color:purple;">基于Transformer编码器更深的自监督模型BERT</mark>
