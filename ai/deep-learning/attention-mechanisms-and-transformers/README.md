# Attention Mechanisms and Transformers

## 大纲

* 首先回顾一个经典注意力框架，解释如何在视觉场景中展开注意力。 受此框架中的_注意力提示_（attention cues）的启发， 我们将设计能够利用这些注意力提示的模型。 1964年的Nadaraya-Waston核回归（kernel regression）正是具有 _注意力机制_（attention mechanism）的机器学习的简单演示。
* 然后继续介绍的是注意力函数，它们在深度学习的注意力模型设计中被广泛使用。 具体来说，我们将展示如何使用这些函数来设计_Bahdanau注意力_。 Bahdanau注意力是深度学习中的具有突破性价值的注意力模型，它双向对齐并且可以微分。
* 最后将描述仅仅基于注意力机制的_Transformer_架构， 该架构中使用了_多头注意力_（multi-head attention） 和_自注意力_（self-attention）。 自2017年横空出世，Transformer一直都普遍存在于现代的深度学习应用中， 例如语言、视觉、语音和强化学习领域。



## Transformer Family Summary

[https://huggingface.co/docs/transformers/en/model\_summary](https://huggingface.co/docs/transformers/en/model\_summary)



Reference

* [https://datawhalechina.github.io/learn-nlp-with-transformers/#/./%E7%AF%87%E7%AB%A02-Transformer%E7%9B%B8%E5%85%B3%E5%8E%9F%E7%90%86/2.3-%E5%9B%BE%E8%A7%A3BERT](https://datawhalechina.github.io/learn-nlp-with-transformers/#/./%E7%AF%87%E7%AB%A02-Transformer%E7%9B%B8%E5%85%B3%E5%8E%9F%E7%90%86/2.3-%E5%9B%BE%E8%A7%A3BERT)
* [https://github.com/datawhalechina/leedl-tutorial](https://github.com/datawhalechina/leedl-tutorial)
* [https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1244/slides/cs224n-2024-lecture08-transformers.pdf](https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1244/slides/cs224n-2024-lecture08-transformers.pdf)
* [https://www.youtube.com/watch?v=wzfWHP6SXxY\&list=PLoROMvodv4rMFqRtEuo6SGjY4XbRIVRd4\&index=7](https://www.youtube.com/watch?v=wzfWHP6SXxY\&list=PLoROMvodv4rMFqRtEuo6SGjY4XbRIVRd4\&index=7)
* [https://udlbook.github.io/udlbook/](https://udlbook.github.io/udlbook/)， 他的slide很不错
* [https://www.borealisai.com/research-blogs/tutorial-14-transformers-i-introduction/](https://www.borealisai.com/research-blogs/tutorial-14-transformers-i-introduction/) 和前面类似的讲义
* [https://blog.csdn.net/hy592070616/article/details/131361891](https://blog.csdn.net/hy592070616/article/details/131361891) 国内讲的还行的







