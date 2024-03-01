# Summary

### What is for ?

* insider for user review fo a product in Amazon Main Topic
* data size: 300MB(megabyte)

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

* From LDA, we can see from the customer review: topics are about good, nice ,beauti, etc
* From K-means, we can see also love, nice, good, but it is not cheap.
