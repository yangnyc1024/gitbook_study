# Attention and Kernel

## 自主vs非自主（是否有任务）

* 非自主性提示是基于环境中物体的突出性和易见性。 想象一下，假如我们面前有五个物品： 一份报纸、一篇研究论文、一杯咖啡、一本笔记本和一本书。 所有纸制品都是黑白印刷的，但咖啡杯是红色的。 换句话说，这个咖啡杯在这种视觉环境中是突出和显眼的， 不由自主地引起人们的注意。 所以我们会把视力最敏锐的地方放到咖啡上。
* 喝咖啡后，我们会变得兴奋并想读书， 所以转过头，重新聚焦眼睛，然后看看书。此时选择书是受到了认知和意识的控制， 因此注意力在基于自主性提示去辅助选择时将更为谨慎。 受试者的主观意愿推动，选择的力量也就更强大。

## Queries, Keys, and Values

* 首先，考虑一个相对简单的状况， 即只使用非自主性提示。&#x20;
* 要想将选择偏向于感官输入， 则可以简单地使用参数化的全连接层， 甚至是非参数化的最大汇聚层或平均汇聚层。
* 因此，“是否包含自主性提示”将注意力机制与全连接层或汇聚层区别开来。&#x20;
  * 在注意力机制的背景下，自主性提示被称&#x4E3A;_&#x67E5;询_（query）。 给定任何查询，注意力机制通&#x8FC7;_&#x6CE8;意力汇聚_（attention pooling） 将选择引导&#x81F3;_&#x611F;官输入_（sensory inputs，例如中间特征表示）。&#x20;
  * 在注意力机制中，这些感官输入被称&#x4E3A;_&#x503C;_（value）。&#x20;
  * 更通俗的解释，每个值都与一&#x4E2A;_&#x952E;_（key）配对， 这可以想象为感官输入的非自主提示。如图所示，可以通过设计注意力汇聚的方式， 便于给定的查询（自主性提示）与键（非自主性提示）进行匹配， 这将引导得出最匹配的值（感官输入）。
*

    <figure><img src="../../../.gitbook/assets/Screenshot 2024-02-14 at 2.33.19 PM.png" alt="" width="375"><figcaption></figcaption></figure>

## Nadaraya-Watson kernel regression & Gaussian Kernel

Nadaraya ([Nadaraya, 1964](https://zh.d2l.ai/chapter_references/zreferences.html#id114))和 Watson ([Watson, 1964](https://zh.d2l.ai/chapter_references/zreferences.html#id180))提出了一个更好的想法， 根据输入的位置对输出$$y_i$$进行加权：$$f(x) = \sum_{i = 1}^{n} \frac{K(x-x_i)}{\sum_{j = 1}^nK(x- x_j)} y_i$$， 其中$$K$$&#x662F;_&#x6838;_（kernel）。&#x20;

* 公式所描述的估计器被称为 _Nadaraya-Watson核回归_（Nadaraya-Watson kernel regression）。

但受此启发， 我们可以从之前图中的注意力机制框架的角度 重写这个核公式， 成为一个更加通用&#x7684;_&#x6CE8;意力汇聚_（attention pooling）公式输出

&#x20;                                                                          $$f(x) = \sum_{i = 1}^{n} \alpha(x, x_i)y_i$$

* 其中$$x$$是查询，$$(x_i, y_i)$$是键值对。
* 注意力汇聚是$$y_i$$的加权平均。
* &#x20;将查询$$x$$和键$$x_i$$之间的关系建模为 _注意力权重_（attention weight）$$\alpha(x,x_o)$$， 如图所示， 这个权重将被分配给每一个对应值$$y_i$$。&#x20;
* 对于任何查询，模型在所有键值对注意力权重都是一个有效的概率分布： 它们是非负的，并且总和为1for example, $$f(x) = \sum_{i = 1}^{n} softmax(-\frac{1}{2}(x-x_i)^2)y_i$$, where 这里使用Gaussian kernel

