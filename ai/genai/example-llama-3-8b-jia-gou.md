---
description: Llama3
---

# Example: Llama 3 8B架构

## Self attention and FFN

注意力层：首先，输入数据会进入self attention layer。在这里，模型使用自我注意力机制来分析数据中的相关性，决定哪些是重要的。这一步骤帮助模型理解不同特征之间的关系

前馈网络（FFN）：在注意力层处理后，得到的新特征会传递到前馈网络。这个网络对每个位置的特征进行进一步处理，通常保罗一些线性变化和非线性激活函数（ReLU），从而生成特征输出



<figure><img src="../.gitbook/assets/Screenshot 2025-03-06 at 10.17.48 PM.png" alt=""><figcaption></figcaption></figure>

在理解数据进入模型之后，我们来思考下关于模型的参数理解

Layers:&#x20;

* 这是现有的transformer的基本构件，举个例子，比如我们前面提到的attention layer和FFN，就都是layers，layer是一个接着一个叠加起来，比如说前面提到数据先进入attention layer，然后传到Poisiton-wise feed-forward network layer，一步一步来处理数据
* 我们常提到transformer有32层，这里指的是我们有32个独立的transformer layer，而这其中每一层都至少含有attention layer和FFN layer

Attention heads:

* 这个是self attention机制中的一部分。每个head独立扫描并且输入序列并且执行注意力步骤（QK-module，softmax函数）

Vocabulary words:

* vocalbulary指的是模型识别或者知道的单词数量。本质上，可以认为这是累累构建词汇库的方式，以至于我们在语言中发展知识和多样性。
* 通常情况下，词汇量越大，模型性能越好

Feature dimension

* 是指数据集中用于描述每个样本的特征数量，即输入数据的维度
* 从传统ml 模型的理解角度来说，就是你一个数据，一条数据，本身所拥有的feature
* 比如说在一个nlp任务重，如果一个词表示为300维的词向量（word2vec, glove），那么它的feature dimension就是300
* 比如说在vision任务重，输入图像时224\*224\*3（宽度，高度，RGB通道），那么输入数据的feature dimension 为224\*224\*3

Hidden dimensions

* 这是模型内部层数的维度，比如说前面提到的feed-forward layers的隐藏层的大小。
* 通常情况下，这些层的大小可以大于feature dimension，帮助模型提取和处理更复杂的数据表示

Context-window size

* 指模型在任何给定时间可处理的单词总数量

那么我们在llama 3-8b的实际参数





<figure><img src="../.gitbook/assets/Screenshot 2025-03-06 at 10.45.51 PM.png" alt=""><figcaption></figcaption></figure>



1） 上下文窗口（context-window）

在实例化llama类的时候，变量max\_seq\_len定义了context-window。类重还有其他参数，但这个参数与transform模型的关系最为直接。这里的max\_seq\_len是8k

<figure><img src="../.gitbook/assets/Screenshot 2025-03-06 at 10.48.10 PM.png" alt=""><figcaption></figcaption></figure>

2）词汇量（Vocabulary-size）和注意力层（Attention Layers）

接下来是transform类，它定义了词汇量和层数。这里的词汇量是指模型能够识别和处理的单词（和tokens）集。Attention layers指的是模型中使用的transformer block（attention和feed-forward layer的组合）

<figure><img src="../.gitbook/assets/Screenshot 2025-03-06 at 10.50.54 PM.png" alt=""><figcaption></figcaption></figure>

根据这些数字，LlaMa 3的词汇量为128k，这是相当大。此外它有32个transformer block



3）特征维度（feature - dimension）和注意力头（attention-heads）

特征维度和attention-heads被引入到self-attention模块中。feature dimension指的是嵌入空间中tokens的向量大小，而attention-heads包括驱动transformers中self-attention机制的QK-module

<figure><img src="../.gitbook/assets/Screenshot 2025-03-06 at 10.59.00 PM.png" alt=""><figcaption></figcaption></figure>

4）隐藏维度（Hidden Dimensions）

&#x20;隐藏维度出现在feed-forward类中，指定了模型中隐藏层的数量。对于LlaMa 3，隐藏层的大小是特征维度的1.3倍。更多的隐藏层数量允许网络在将他们投射回较小的输出维度之前，内部创建和操纵更丰富的表示。

<figure><img src="../.gitbook/assets/Screenshot 2025-03-06 at 11.01.19 PM.png" alt=""><figcaption></figcaption></figure>

5）transformer

第一个矩阵是输入特征矩阵，通过attention layer处理生成attention weighted features。

这里的输入特征矩阵只有5\*3。但是在真实的llama 3模型汇总，它增长到8k\*4096

feed-forward network中的隐藏层，增长到5325，然后在最后一层回落到4096



<figure><img src="../.gitbook/assets/Screenshot 2025-03-06 at 11.03.52 PM.png" alt=""><figcaption></figcaption></figure>

6）transformer block中的多层

llama3结合了上述的32个transformer block，输出从一个block传递到下一个block，直到达到最后一个block

7）把前面提到的所有放在一起

<figure><img src="../.gitbook/assets/Screenshot 2025-03-06 at 11.05.45 PM.png" alt=""><figcaption></figcaption></figure>

* 首先我们有我们的输入矩阵，大小为8k（context-window）\* 128k（vocabulary-size）/这个矩阵经过嵌入处理，将这个高维矩阵转换为低维
* 其次，在这种情况下，这个低维结果变成了4096，这是我们之前看到的llama模型中特征的指定维度
* 第三部，这个特征通过transformer block进行处理，首先由attention layer处理，然后ffn layer。aattention layer 横向夸特征处理，而ffn layer则是纵向跨维度处理
* 步骤3为transformer block的32层重复。最终，结果矩阵的维度与用于特征维度的维度相同
* 最后，这个矩阵被转换为原始的词汇矩阵大小，就是128k，以便于模型可以选择并映射词汇中可用的单词



总结一下

* max\_seq\_len (最大序列长度) 这是模型在单次处理时能够接受的最大token数。 在LlaMa 3-8B模型中，这个参数设定为8,000个tokens，即Context Window Size = 8K。这意味着模型在单次处理时可以考虑的最大token数量为8,000。这对于理解长文本或保持长期对话上下文非常关键。
* Vocabulary-size (词汇量) 这是模型能识别的所有不同token的数量。这包括所有可能的单词、标点符号和特殊字符。模型的词汇量是128,000，表示为Vocabulary-size = 128K。这意味着模型能够识别和处理128,000种不同的tokens，这些tokens包括各种单词、标点符号和特殊字符。
* Vocabulary-size (词汇量) 这是模型能识别的所有不同token的数量。这包括所有可能的单词、标点符号和特殊字符。模型的词汇量是128,000，表示为Vocabulary-size = 128K。这意味着模型能够识别和处理128,000种不同的tokens，这些tokens包括各种单词、标点符号和特殊字符。
* transformer block 包含多个不同层的模块，通常至少包括一个Attention Layer和一个Feed-Forward Network（前馈网络）。一个模型可以有多个transformer block，这些block顺序连接，每个block的输出都是下一个block的输入。&#x20;
  * 在Transformer模型的语境中，通常我们说模型有“32层”，这可以等同于说模型有“32个Transformer blocks”。
  * 每个Transformer block通常包含一个自注意力层和一个前馈神经网络层，这两个子层共同构成了一个完整的处理单元或“层”。 因此，当我们说模型有32个Transformer blocks时，实际上是在描述这个模型由32个这样的处理单元组成，每个单元都有能力进行数据的自注意力处理和前馈网络处理。这种表述方式强调了模型的层级结构和其在每个层级上的处理能力。&#x20;
  * 总结来说，"32层"和"32个Transformer blocks"在描述Transformer模型结构时基本是同义的，都指模型包含32次独立的数据处理周期，每个周期都包括自注意力和前馈网络操作。
* Feature-dimension (特征维度) 这是输入token在模型中表示为向量时，每个向量的维度。 每个token在模型中被转换成一个含4096个特征的向量，即Feature-dimension = 4096。这个高维度使得模型能够捕捉更丰富的语义信息和上下文关系
* Attention-Heads (注意力头) 在每个Attention Layer中，可以有多个Attention-Heads，每个head独立地从不同的视角分析输入数据。 每个Attention Layer包含32个独立的Attention Heads，即Number of Attention Heads = 32。这些heads分别从不同的方面分析输入数据，共同提供更全面的数据解析能力。
* Hidden Dimensions (隐藏维度) 这通常指的是在Feed-Forward Network中的层的宽度，即每层的神经元数量。通常，Hidden Dimensions会大于Feature-dimension，这允许模型在内部创建更丰富的数据表示。 在Feed-Forward Networks中，隐藏层的维度为5325，即Hidden Dimensions = 5325。这比特征维度大，允许模型在内部层之间进行更深层次的特征转换和学习。
  * 关系和数值： Attention Layers 和 Attention-Heads 的关系：每个Attention Layer可以包含多个Attention-Heads。&#x20;
  * 数值关系：一个模型可能有多个transformer blocks，每个block包含一个Attention Layer和一个或多个其他层。每个Attention Layer可能有多个Attention-Heads。这样，整个模型就在不同层和heads中进行复杂的数据处理。



## Reference

* [https://www.53ai.com/news/qianyanjishu/1867.html](https://www.53ai.com/news/qianyanjishu/1867.html)
* [https://zhuanlan.zhihu.com/p/693323342](https://zhuanlan.zhihu.com/p/693323342)
