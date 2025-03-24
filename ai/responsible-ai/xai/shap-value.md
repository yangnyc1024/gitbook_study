# SHAP value

## What is SHAP value?

We are interested in understanding how each feature contributes to a prediction. In linear models, this is relatively straightforward to compute. Consider a linear model:

$$
\hat{f}(x) = \beta_0 + \beta_1 x_1 + \cdots + \beta_p x_p
$$

where $$x$$ is the input instance we want to explain, each $$x_j$$ for ( $$j = 1, \ldots, p$$ ) is the feature value, and ( $$\beta_j$$ ) is the coefficient corresponding to feature $$j$$.

The contribution of the $$j$$-th feature to the prediction ( $$\hat{f}(x)$$ ) is defined as:

$$
\phi_j = \beta_j x_j - \mathbb{E}(\beta_j X_j) = \beta_j x_j - \beta_j \mathbb{E}(X_j)
$$

Here, ( $$\mathbb{E}(\beta_j X_j$$) denotes the average contribution of the $$j$$-th feature. The contribution measures how much **this feature deviates from its average impact**. If we sum the contributions of all features for a given instance, we obtain:

$$
\sum_{j=1}^p \phi_j = \sum_{j=1}^p (\beta_j x_j - \mathbb{E}(\beta_j X_j)) \\
= \left( \beta_0 + \sum_{j=1}^p \beta_j x_j \right) - \left( \beta_0 + \sum_{j=1}^p \mathbb{E}(\beta_j X_j) \right) \\
= \hat{f}(x) - \mathbb{E}(f(X))
$$

In other words, the total contribution of input $$x$$ is equal to the prediction minus the average prediction. Since we often work with non-linear models (e.g., ensemble methods), we require a more general approach. We adopt the **Shapley value** from cooperative game theory to attribute the prediction of any machine learning model to individual feature contributions.

The Shapley value of feature $$j$$ for an instance is defined as:

$$
\phi_j(val) = \sum_{S \subseteq \{x_1, \ldots, x_p\} \setminus \{x_j\}} \frac{|S|!(p - |S| - 1)!}{p!} \left[ val(S \cup \{x_j\}) - val(S) \right]
$$

Here:

* $$S$$ is a subset of the full set of features (a _coalition_),
* $$x$$ is the feature vector of the instance being explained,
* $$p$$is the total number of features,
* $$\frac{|S|!(p - |S| - 1)!}{p!}$$ is the Shapley weight for subset ( S ),
* $$val(S)$$ is the value function (i.e., model output) for feature subset $$S$$, marginalized over the features not in $$S$$. The value function $$val_x(S)$$ is computed as:

$$
val_x(S) = \int f(x_1, \ldots, x_p) \, dP_{x_{\notin S}} - \mathbb{E}_X[\hat{f}(X)]
$$

* **This expression marginalizes over the features** not included in $$S$$. For example, suppose the model uses 4 features $$x_1, x_2, x_3, x_4$$, and we consider the coalition $$S = {x_1, x_3}$$. Then the value function is:

$$
val_x(S) = \int_{\mathbb{R}} \int_{\mathbb{R}} f(x_1, X_2, x_3, X_4) \, dP_{X_2, X_4} - \mathbb{E}_X[\hat{f}(X)]
$$





## What is baseline?

在 TreeSHAP 中，baseline（有时也叫 **expected value**）是：

> **模型在训练集或测试集上所有预测值的平均值**，即\
> $$baseline=E[f(x)]$$

* 对于回归问题：就是所有样本预测值的平均值。
* 对于二分类（log-odds 模型）：是 logit 输出的平均值。
* 对于概率输出（经过 sigmoid）模型：可以取平均概率作为 baseline（但 TreeSHAP 默认是在 log-odds 上计算）。



## What is the SHAP additive?

**SHAP 是加性的，但不代表模型是线性的**

SHAP 的核心数学基础是 **Shapley value**，满足以下属性：

> 对于任意模型 $$f(x)$$，我们可以写成：
>
> $$f(x) = \phi_0 + \sum_{i = 1}^M \phi_i$$
>
> 其中：
>
> * $$\phi_0$$​ 是 baseline（即 $$\mathbb{E}[f(x)]$$）
> * $$\phi_i$$​ 是第 $$i$$ 个特征对模型输出的边际贡献（SHAP 值）

## SHAP value  VS linear coefficient

* 在线性模型中，**系数** $$\beta$$ **是模型本身学出来的参数**。
  * 它反映的是**每个特征单位变化**对输出的直接影响。
  * 和特征标准化、缩放、共线性密切相关。
* 在 SHAP 中，$$\phi$$ **是模型预测后计算出来的归因值。**
  * 它不是模型的参数，而是解释模型预测的“分摊结果”。
  * 会随着特征值、样本、模型结构、甚至特征顺序而变化。



#### 假设你有一个模型预测：

**💡 线性模型：**

$$\text{premium} = \beta_0 + 0.8 \cdot \text{age} + 2.5 \cdot \text{claim\_count}$$

* 不论样本是年轻还是年老，`age` 的单位贡献永远是每多一岁 → 保费涨 0.8 元。
* 模型结构是“全局一致的”。

**💡 非线性模型（如 XGBoost）+ SHAP：**

* 对年轻人，`age` 的 SHAP 值可能是 -1.0 → 降低保费；
* 对年长的人，`age` 的 SHAP 值可能是 +3.0 → 提高保费；
* 说明模型对 `age` 的使用是非线性、有阈值的（比如 60 岁以上风险变大）。

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-24 at 4.03.48 PM.png" alt=""><figcaption></figcaption></figure>



## Extra

* mean SHAP value 不等同于线性模型中的系数或贡献，它是对特征在整个样本空间中边际贡献的平均估计。虽然 SHAP decomposition 在形式上是加性的，但它能捕捉模型中复杂的非线性和特征交互，从而为任意模型提供一致的解释。
* The **mean SHAP value** reflects the feature’s **average marginal contribution** to the model output across all data points. A decrease in this value suggests that the model is now **less reliant on this feature** and **more dependent on other variables** to explain the predictions.\
  However, this does **not imply a consistent 15% contribution** as would be the case in a linear model with fixed coefficients. For example, the SHAP value of a feature could account for 10% of the prediction in one data point, and 25% in another — highlighting the **local, context-specific nature** of SHAP-based explanations.



Reference

* [https://christophm.github.io/interpretable-ml-book/shap.html](https://christophm.github.io/interpretable-ml-book/shap.html)&#x20;
* [https://zhuanlan.zhihu.com/p/85791430](https://zhuanlan.zhihu.com/p/85791430)
