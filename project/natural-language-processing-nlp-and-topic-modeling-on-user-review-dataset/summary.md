# Summary

### What is for ?

* insider for user review fo a product in Amazon Main Topic
* data size: 300MB(megabyte)
*

    <figure><img src="../.gitbook/assets/Screen Shot 2021-08-17 at 2.21.41 PM.png" alt="" width="375"><figcaption></figcaption></figure>

### What have done?

#### Preprocess the customer reviews by Tokenizing

* （将文本(例如一个句子)分解成单独的词语(通常是单词)的过程。） and Stemming（词干抽取、词根提取）
* 注意一些we 这样的词语
* 注意本身具有的关键词

#### Extract the feature and build the TF-IDF matrix

* 具体解释？TF: Term Frequency - IDF: Inverse Document Frequency

#### Train unsupervised learning model by K-Means and Latent Dirichlet Allocation Algorithm

* LDA：用linear algebra直接找出里面的main topics(from the dictionary in each review)
* cluster：找tf-idf的中心值

#### Result Evaluation

* From LDA, we can see from the customer review topics are about good, nice ,beauty, etc
* From K-means, we can also see love, nice and good, but it is not cheap.

Reference:

[https://zhuanlan.zhihu.com/p/103438436\
\
https://zhuanlan.zhihu.com/p/31470216](https://zhuanlan.zhihu.com/p/103438436https:/zhuanlan.zhihu.com/p/31470216)
