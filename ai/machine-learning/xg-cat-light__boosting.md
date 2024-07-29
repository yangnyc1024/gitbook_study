# XG,Cat,Light\_\_Boosting

## XGboosting

### 什么是xgboosting

* Xgboosting本质上还是一个gbdt，但是努力的把速度和效率发挥到了极致，所以就被取名是X（Extreme）
* 从损失函数的角度提出的，它在损失函数里加入了正则惩罚项，同时认为单单求偏导还不够.因为求偏导实际是一阶泰勒展开,属于一阶优化，收敛速度还不够快.他提出了损失函数二阶泰勒展开式的想法.

### Xgboosting树的定义



### Xgboosting 背后的数学

#### Review CART

Here’s a simple example of a CART that classifies whether someone will like a hypothetical computer game X. The example of tree is below:

The prediction scores of each individual decision tree then sum up to get  If you look at the example, an important fact is that the two trees try to _complement_ each other. Mathematically, we can write our model in the form

&#x20;                                                                $$\hat{y_i} = \sum_{k=1}^K f_k (x_i), f_k \in \mathcal{F}$$

where, K is the number of trees, $$f$$ is the functional space of $$F$$, $$F$$ is the set of possible CARTs.

The objective function for the about model is given by:

&#x20;                                                             $$obj(\theta) = \sum_{i= 1}^n(y_i, \hat{y_i}) + \sum_{k=1}^K \Omega(f_k)$$

where, first term is the loss function and the second is the regularization parameter.

#### Xgboosting

Now, Instead of learning the tree all at once which makes the optimization harder, we apply the additive strategy, minimize the loss what we have learned and add a new tree which can be summarised below:

$$\hat{y}_i^{(0)} = 0,  \hat{y}_0^{(1)} = f_1(x_i) =$$











xgboosting的核心算法

* 就是不停的添加树，不断地进行特征分裂来生长一棵树，每次添加一个树。其实就是学习一个新的函数，去预测之前的残差
* 当我们训练完成后得到的k棵树，我们要预测一个样本的分数，其实就是根据地这个样本的特征，在每棵树中会落到对应的一个叶子节点，每个叶子节点就对应一个分数
* 最后只需要将每棵树对应的分数加起来就是该样本的预测值
*























## Catboosting



## LightBoosting







## Reference

* [https://mayuanucas.github.io/xgboost-lightgbm/](https://mayuanucas.github.io/xgboost-lightgbm/)
* [https://github.com/NLP-LOVE/ML-NLP/tree/master/Machine%20Learning/3.3%20XGBoost](https://github.com/NLP-LOVE/ML-NLP/tree/master/Machine%20Learning/3.3%20XGBoost)
* [https://blog.csdn.net/v\_JULY\_v/article/details/81410574](https://blog.csdn.net/v\_JULY\_v/article/details/81410574)
* [https://www.geeksforgeeks.org/xgboost/](https://www.geeksforgeeks.org/xgboost/)
