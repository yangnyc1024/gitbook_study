# Model Evaluation

## Overfitting

### what is overfitting?

* 如果模型在训练数据上表现很好，反而在未知的数据表现的不太好，这就出于overfitting（这里是连接training和）

### 什么情况出现overfitting？

* Q1: Is the more complicated the better?
* Q2: In classification problems. are our features the more the better?（features多余你的data）
* Fundamental causes of overfittng:

### bias/variance/error/model error

* 学生的考试能力 = 你的平均水平（与这一次没有关系）+这一次的发挥来说对你多正常
* 模型的精准性bias：
  * 第一层次的理解：模型输出结果与真实值之间的差距。错误！！！
  * 第二层次的理解：这个model在训练数据有变化下的平均输出结果与真实值相比，得到的平均准确性
* 模型的稳定性variance：
  * 第一层次的理解：模型输出结果的稳定性
  * 第二层次的理解：’某一次model的数据结果与这次model的平均水平的差距‘的平方的期望
* Q：那你怎么从一个training的bias 和variance去看model本身的bias和variance呢？
  * trade off?

## Model Error

### what is model error?

* 是在test error上
* loss function 是用来构造模型；model error 是用来检查模型效果的

## How to solve the overfitting problem？

* Increase traning data size
* avoid over-traning your dataset:
  * Filter out features, e.g. feature reduction
    * Principal component analysis(PCA)
  * Regularization
    * Ridge regression, Least absolute shrinkage and selction operation(LASSO)
    * Logistic Regression-L2, Logistic Regression-L1
  * Ensemble Learning

## Regularization

情况

### Ridge Regression: L2 penalty in loss function

* 这样的penalty公式中的 就是hyperparameter：
  * 可以让方差和偏差达到平衡：增大，模型方差（variance）减少，偏差增大（bias）

### LASSO: L1 penalty in loss function

### Hyperparameter Optimization

* 这样的penalty公式中的$$\lambda$$​​​​​​​就是hyperparameter：
  * $$\lambda$$​​​​​​​可以让方差和偏差达到平衡：增大，模型方差（variance）减少，偏差增大（bias）
  * $$\lambda$$​​​​​​​相当于你在用来控制你的参数a和b
* 总结：
  * L1:：feature selection regulariation
  * L2：是correlation的情况处理的比较好
  * model error 不存在training上，mse是用来测试机器好不好，所以不是不用Regularization
  * L1和L2一般就用在linear 和logistics上现在，不过Regularization这个概念在其他地方都有

## 一些调参数的过程的思考
