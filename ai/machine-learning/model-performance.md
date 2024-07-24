# Model Performance

## 1 Why do model evaluation?

* 这个部分相当于是你做完clean/feature engineering/ model，就到model evaluation了，说白了就是说，你模型到底如何
* 对应<mark style="color:purple;">How can we compare this model with others model?</mark>



## 2 How to evaluate a model?

### What data to evaluate

* select and split data

### What method to use（实验评估方法/Model Selection）

#### Cross Validation

* What is Cross Validation?
  * Assess how your model result will generalize to another independent data set.
  * Predict and test on the same data is a methodological mistake
  * There are several cross validation techniques, popular is k-fold cross validation

#### K-fold Cross Validation

### What metrics to compare（性能度量performance measure）

#### Classification-Confusion matrix

* picture![](https://api2.mubu.com/v3/document\_image/2dbf066c-6490-46f5-ac78-24dbb11add0b-12267179.jpg)
* TP/FN/FP/TN；True/False；Postive/Negative
  * TP: true positive（真正例）; FN: false negative（假反例）(type II)
  * FP: false positive（假正例type I）; TN: true negative（真反例）
  * **True/False** means if you made a correct/wrong prediction
  * **Positive/Negative** means what your prediction is/is not
* Accuracy
  * $$\frac{TP+TN}{TP+TN+FP+FN}$$​​​​​​​​​​​​​​​​​​​​​​​​​​
  * 预测中你对的多少个
* Precision
  * $$P=\frac{TP}{TP+FP}$$​​​​​​​​​​​​​​​​​​​
  * 查准率precision：你说的准确到底有多少可以相信的
  * 在所有你认为positive的数据中，有多少真的是positive？
  * example, spam email：要求precision高（杀的必须准）
* Recall Sensitivity
  * $$R=\frac{TP}{TP+FN}$$
  * （查全率recall：真的是不是都预测对了）查全率recall：真的是不是都预测对了
  * 在所有positive的数据中，有多少被你正确地识别出来（是positive）
  * disease/cybersecuirity：要求recall高( 宁可错杀)
  * 如果negative很重要，你看recall，反之你看precision更关注positive
* F1
  * $$F1=\frac{2TP}{2TP+FP+FN}=\frac{2}{\frac{1}{recall}+\frac{1}{precision}}$$
  * (可以统一recall\&precision)
  * 越高越好

#### Classification-ROC

* Receiver operation characteristic curve（根据你的threshold来制定的，threshold是用来就判断是positive or negative，像logistic regression里，我高于0.8,判定为positive，当然你可以选0.6）
* Define False Positive Rate as X axis, True Positive Rate as Y axis
* The receiver operating curve, also noted ROC, is the plot of TPR versus FPR by varying the threshold.
* Special Points in ROC space
  * best case(0,1); worst case:(1,0)
  * 对角线上的点：
    * 当threshold设定为最高时，所有样本都被预测为negative，此时得到的点在(0,0).
    * 当threshold设定为最低时，所有样本都被预测为positive，此时得到的点在(1,1)
  * why does Equal Error rate mean FPR = FNR?
    * 已知固定关系： FNR=1-TP/Number of real positive = 1- TPR
    * 根据图中焦点性质可知： FPR （x）= 1-TPR（y）
    * FPR=FNR

#### Classification-AUC

* 你想完整的表示前面的auc么？
  * Area under the curve of ROC(AUC)
  * AUC value: \[0,1]
  * The larger the value is, the better classification performance your classifier has.
  * AUC value is a probability value.
* 面试题：机器学习里0-1的值，都希望有一个概率。怎么用概率来解释AUC？
  * ROC AUC is the probability that a randomly-chosen positive example is ranked more highly than a randomly-chosen negative example.

#### Regression

* ERM，empirical risk measure：
* coefficient of determination

## 3 Failures Analysis&#x20;

* 不同的策略来解决减少failures（把你的failures的分类）
  * 可以通过模型解决
  * 可以通过调参解决
  * 可以通过data解决(可能你少一部分data)
  * 不能解决
* failures analysis的目的就是进一步提高模型的性能，进行迭代开发，retraining
* Summary
  * cross validation——找骨架（model selection/model infrastructure）
  * mixed validation and training data into training——找肉，例如y=ax+b里面的a和b
  * model evaluation——ROC，AUC，Precision，Recall
  * failure analysis——确定问题在哪里，然后更新step1-3

## Machine Learning End-to-End Pipeline

### Business Design

### Data acquisition

* collect data from outside system
* pre-process into the format that needed

### Data preparation

* Clean, transform, validate and select data
* annotation
* feature extraction
* prepare data into: training, validation and evaluation datasets

### Training & Validation

* Select the model
* Train the model
* Tune the model
* Validate the training process

### Testing Evaluation

* evaluate the performance metrics on the evaluation dataset
* analyze failures

### Deployment& Inference

* Integrated into production apps
* config models based on system needs
* predict on real-life data
* log failures/errors

