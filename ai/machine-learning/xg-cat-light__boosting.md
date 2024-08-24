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

$$\hat{y}_i^{(0)} = 0$$&#x20;

$$\hat{y}_i^{(1)} = f_1(x_i) =\hat{y}_i^{(0)} + f_1(x_i)$$　

$$\hat{y}^{(2)}_i = f_1(x_i) + f_2(x_i) = \hat{y}^{(1)}_i + f_2(x_i)$$

The objective function of the above model can be defined as:

$$obj^{(t)} = \sum_{i=1}^{n} l(y_i, \hat{y}^{(t)}_i) + \sum_{i=1}^{t} \Omega(f_i) = \sum_{i=1}^{n} l(y_i, \hat{y}^{(t-1)}_i + f_t(x_i)) + \Omega(f_t) + constant$$\


$$obj^{(t)} = \sum_{i=1}^{n} (y_i - (\hat{y}^{(t-1)}_i + f_t(x_i)))^2 + \sum_{i=1}^{t} \Omega(f_i) = \sum_{i=1}^{n} [2(y_i - \hat{y}^{(t-1)}_i) f_t(x_i) + f_t(x_i)^2] + \Omega(f_t) + constant ]$$

Now, let’s apply the Taylor series expansion up to the second order:

$$obj^{(t)} = \sum_{i=1}^{n} [l(y_i, \hat{y}^{(t-1)}_i) + g_i f_t(x_i) + \frac{1}{2} h_i f_t^2(x_i)] + \Omega(f_t) + constant$$

where g\_i and h\_i can be defined as:

$$g_i = \frac{\partial l(y_i, \hat{y}^{(t-1)}_i)}{\partial \hat{y}^{(t-1)}_i}$$

$$h_i = \frac{\partial^2 l(y_i, \hat{y}^{(t-1)}_i)}{\partial \hat{y}^{(t-1)}_i}$$

Simplifying and removing the constant:

$$\sum_{i=1}^{n} [g_i f_t(x_i) + \frac{1}{2} h_i f_t^2(x_i)] + \Omega(f_t)$$



Regularization

Now, we define the regularization term, but first we need to define the model:

$$ft(x) = w_{q(x)}, w \in R^T, q : R^d \rightarrow {1, 2, ..., T}$$

Here, w is the vector of scores on leaves of tree, q is the function assigning each data point to the corresponding leaf, and T is the number of leaves. The regularization term is then defined by:

$$\Omega(f) = \gamma T + \frac{1}{2} \lambda \sum_{j=1}^{T} w_j^2$$

Now, our objective function becomes:

$$obj^{(t)} \approx \sum_{i=1}^{n} [g_i w_{q(x_i)} + \frac{1}{2} h_i w_{q(x_i)}^2] + \gamma T + \frac{1}{2} \lambda \sum_{j=1}^{T} w_j^2 = = \sum_{j=1}^{T} \left( \left( \sum_{i \in I_j} g_i \right) w_j + \frac{1}{2} \left( \sum_{i \in I_j} h_i + \lambda \right) w_j^2 \right) + \gamma T ]$$

Now, we simplify the above expression:

$$obj^{(t)} = \sum_{j=1}^{T} \left( G_j w_j + \frac{1}{2} (H_j + \lambda) w_j^2 \right) + \gamma T$$

where,

$$G_j = \sum_{i \in I_j} g_i$$

$$H_j = \sum_{i \in I_j} h_i$$

In this equation, w\_j are independent of each other, the best ![w\_j](https://www.geeksforgeeks.org/wp-content/ql-cache/quicklatex.com-0a9d7fe27854af070301d3307810c89f\_l3.svg) for a given structure q(x) and the best objective reduction we can get is:

$$w_j^* = -\frac{G_j}{H_j + \lambda}$$&#x20;

$$obj^* = -\frac{1}{2} \sum_{j=1}^{T} \frac{G_j^2}{H_j + \lambda} + \gamma T$$&#x20;

where, γ\gammaγ is pruning parameter, i.e., the least information gain to perform split.

Now, we try to measure how good the tree is; we can’t directly optimize the tree, we will try to optimize one level of the tree at a time. Specifically, we try to split a leaf into two leaves, and the score it gains is:

$$Gain = \frac{1}{2} \left( \frac{G_L^2}{H_L + \lambda} + \frac{G_R^2}{H_R + \lambda} - \frac{(G_L + G_R)^2}{H_L + H_R + \lambda} \right) - \gamma$$





xgboosting的核心算法

* 就是不停的添加树，不断地进行特征分裂来生长一棵树，每次添加一个树。其实就是学习一个新的函数，去预测之前的残差
* 当我们训练完成后得到的k棵树，我们要预测一个样本的分数，其实就是根据地这个样本的特征，在每棵树中会落到对应的一个叶子节点，每个叶子节点就对应一个分数
* 最后只需要将每棵树对应的分数加起来就是该样本的预测值



Reference

* [https://www.geeksforgeeks.org/xgboost/](https://www.geeksforgeeks.org/xgboost/)























## Catboosting



## LightBoosting







## Reference

* [https://mayuanucas.github.io/xgboost-lightgbm/](https://mayuanucas.github.io/xgboost-lightgbm/)
* [https://github.com/NLP-LOVE/ML-NLP/tree/master/Machine%20Learning/3.3%20XGBoost](https://github.com/NLP-LOVE/ML-NLP/tree/master/Machine%20Learning/3.3%20XGBoost)
* [https://blog.csdn.net/v\_JULY\_v/article/details/81410574](https://blog.csdn.net/v\_JULY\_v/article/details/81410574)
* [https://www.geeksforgeeks.org/xgboost/](https://www.geeksforgeeks.org/xgboost/)
