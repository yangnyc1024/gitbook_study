# Summary



### What is for

* Small recommendation system
* data set: 100k user rview

#### Part 1: Spark SQL and OLAP

* The number of Users
* The number of Movies
* How many movies are rated by users?
* List movies not rated before
* List Movie Genres Movie for Each Category



#### Part 2: Spark ALS based approach for training model

We will use an Spark ML to predict the ratings, so let's reload "ratings.csv" using `sc.textFile` and then convert it to the form of (user, item, rating) tuples.

1. Data Preprocessing
2.  ALS Model Selection and Evaluation

    1. 2.1off-line
    2. 2.2从协同过滤（collaborate filter）的分类来说，ALS算法属于User-Item CF，也叫做混合CF。它同时考虑了User和Item两个方面。
    3. 2.3 则我们定义Rating矩阵，其中的元素表示第u个User对第i个Item的评分。Rating u(User) \* i(Item)
    4. 2.4 x y就是对应的 user 和 item 以及中间变量 k（可以当作是关联？）

    <figure><img src="../.gitbook/assets/Screen Shot 2021-08-17 at 2.35.13 PM.png" alt="" width="375"><figcaption></figcaption></figure>

    1. 2.5 我们关注的模型由奇异值分解（SVD）推演而来。一个典型的模型将每个用户u（包含一个用户-因素向量ui）和每个商品v（包含一个用户-因素向量vj）联系起来。预测通过内积rij=（uiT）vj来实现。另一个需要关注的地方是参数估计。许多当前的工作都应用到了显式反馈数据集中，这些模型仅仅基于观察到的rating数据直接建模，同时通过一个适当的正则化来避免过拟合。
3. Model testing
4. Model apply and see the performance
   1. from pyspark.ml.evaluation import RegressionEvaluator
   2. from pyspark.ml.recommendation import ALS
   3. from pyspark.ml.tuning import CrossValidator,ParamGridBuilder

#### Part 3: Recommends movie to certainty user with id

#### Part4: Find the similar movies for movie with id

[https://zhuanlan.zhihu.com/p/79338001冷启动，让他们有些评级](https://zhuanlan.zhihu.com/p/79338001%E5%86%B7%E5%90%AF%E5%8A%A8%EF%BC%8C%E8%AE%A9%E4%BB%96%E4%BB%AC%E6%9C%89%E4%BA%9B%E8%AF%84%E7%BA%A7)

[https://zhuanlan.zhihu.com/p/145120275](https://zhuanlan.zhihu.com/p/145120275)&#x20;

你相当于直接补上空白
