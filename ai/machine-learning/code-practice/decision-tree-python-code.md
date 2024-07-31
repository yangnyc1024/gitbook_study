# Decision Tree Python Code



Test data

* 使用三个指标，是否为985，学历，编程语言，来判断是否面试录取

Decision Tree Algorithm

* 将所有指标添加进指标列表
* 计算指标列表中每个指标的熵，并按照最小熵的指标进行划分
* 如果能够成功划分则直接得出结果
  * 否则将该指标从指标列表移除后之前前一个步骤
  * 并且将结果添加到决策树中

````python
```python
import numpy as np
from collections import Counter
from math import log2


# 用于计算信息熵的辅助函数
def entropy(y):
    counter = Counter(y)  # 统计每个类别的样本数量
    total = len(y)  # 样本总数
    ent = 0.0
    for count in counter.values():
        p = count / total  # 计算类别概率
        ent -= p * log2(p)  # 计算信息熵
    return ent

def geni(y_label):
    """
    计算基尼系数

    参数:
    y_label (list): 类别标签列表

    返回:
    float: 基尼系数
    """
    counter = Counter(y_label)  # 统计每个类别的样本数量
    g = 1.0  # 基尼系数初始化为1
    for num in counter.values():
        p = num / len(y_label)  # 计算类别概率
        g -= p * p  # 基尼系数公式
    return g


class DecisionTree:
    def __init__(self):  # 初始化方法
        self.tree = {}  # 初始化决策树为空字典

    # 训练决策树
    def fit(self, X, y):
        cols = list(range(X.shape[1]))  # 获取所有特征列的索引
        # 对X的每一列数据，计算分割后的信息熵
        self.tree = self._genTree(cols, X, y)  # 生成决策树

    # 递归生成决策树
    def _genTree(self, cols, X, y):
        # 计算最小信息熵的特征
        imin = cols[0]  # 最小熵的列
        emin = 100  # 最小熵值，初始化为一个较大值
        for i in cols:
            coli = X[:, i]  # 拿到第i个特征数据，X里面有行和列，行是数据，列是第ith 特征数据
            enti = sum([entropy(y[coli == d]) for d in set(coli)])  # 计算该特征的总熵值，y[coli == d]相当走过所有的这些特征数据？
            if enti < emin:
                imin = i  # 更新最小熵特征列
                emin = enti  # 更新最小熵值
        # 根据最小熵特征有几个值，生成几个新的子树分支
        newtree = {}
        mincol = X[:, imin]  # 获取最小熵特征的数据
        cols.remove(imin)  # 移除已使用的特征列
        # 针对这个特征的每个值，进一步划分树
        for d in set(mincol):
            entd = entropy(y[mincol == d])  # 计算该特征值的熵
            if entd < 1e-10:  # 如果已经完全分开
                newtree[d] = y[mincol == d][0]  # 直接取该特征值的分类结果
            else:  # 还需要进一步细分
                newtree[d] = self._genTree(cols.copy(), X[mincol == d, :], y[mincol == d])  # 递归生成子树
        return {imin: newtree}  # 将列号作为索引，返回新生成的树

    # 预测新样本
    def predict(self, X):
        X = X.tolist()  # 将输入数据转换为列表
        y = [None for i in range(len(X))]  # 初始化预测结果
        for i in range(len(X)):
            predictDict = self.tree  # 从根节点开始预测
            while predictDict != 'Yes' and predictDict != 'No':  # 如果不是叶子节点
                col = list(predictDict.keys())[0]  # 获取当前节点的特征列
                predictDict = predictDict[col]  # 更新预测字典到子树
                predictDict = predictDict[X[i][col]]  # 根据样本特征值选择子树
            else:  # 如果是叶子节点
                y[i] = predictDict  # 记录预测结果
        return y  # 返回所有样本的预测结果
```



````

````python
```python
import numpy as np
from collections import Counter
from math import log2

X=np.array([['Yes985','本科','C++'],
            ['Yes985','本科','Java'],
            ['No985' ,'硕士','Java'],
            ['No985' ,'硕士','C++'],
            ['Yes985','本科','Java'],
            ['No985' ,'硕士','C++'],
            ['Yes985','硕士','Java'],
            ['Yes985','博士','C++'],
            ['No985' ,'博士','Java'],
            ['No985' ,'本科','Java']])
y=np.array(['No','Yes','Yes','No','Yes','No','Yes','Yes','Yes','No'])


# Test data
# 使用三个指标，是否为985，学历，编程语言，来判断是否面试录取
# Decision Tree Algorithm
# 将所有指标添加进指标列表
# 计算指标列表中每个指标的熵，并按照最小熵的指标进行划分
# 如果能够成功划分则直接得出结果
# 否则将该指标从指标列表移除后之前前一个步骤
# 并且将结果添加到决策树中

dt = DecisionTree()
dt.fit(X, y)
print(dt.tree)
print(dt.predict(X))
```
````



Reference:

* [https://juejin.cn/post/7077352935834779685](https://juejin.cn/post/7077352935834779685)
* [https://juejin.cn/post/7077383466655940644](https://juejin.cn/post/7077383466655940644)
