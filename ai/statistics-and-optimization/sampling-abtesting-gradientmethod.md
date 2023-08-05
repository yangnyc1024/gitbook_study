---
description: Google Coding Summary
---

# Sampling/ABtesting/GradientMethod

```python
import numpy as np 
import scipy.stats as st
import seaborn as sns
import matplotlib.pyplot
```

### Linear Regression

#### Linear Skilearn：X\_b = np.c\_\[np.ones((100, 1)), X] 和theta\_best = np.linalg.inv(X\_b.T.dot(X\_b)).dot(X\_b.T).dot(y)

[https://colab.research.google.com/drive/1MnNENQS5j2otC7quOGuqWGHg7DqCXG7g](https://colab.research.google.com/drive/1MnNENQS5j2otC7quOGuqWGHg7DqCXG7g)

```python
####################linear regression sklearn#########################
from sklearn.linear_model import LinearRegression

lin_reg = LinearRegression()
lin_reg.fit(X, y)
lin_reg.intercept_, lin_reg.coef_

theta_best_svd, residuals, rank, s = np.linalg.lstsq(X_b, y, rcond=1e-6)
theta_best_svd

np.linalg.pinv(X_b).dot(y)

###################Least Square ##########################
import numpy as np

X = 2 * np.random.rand(100, 1)
y = 4 + 3 * X + np.random.randn(100, 1)
plt.plot(X, y, "b.")
plt.xlabel("$x_1$", fontsize=18)
plt.ylabel("$y$", rotation=0, fontsize=18)
plt.axis([0, 2, 0, 15])
save_fig("generated_data_plot")
plt.show()

#least square
X_b = np.c_[np.ones((100, 1)), X]  # add x0 = 1 to each instance 
#np.r_是按列连接两个矩阵，就是把两矩阵上下相加，要求列数相等。
#np.c_是按行连接两个矩阵，就是把两矩阵左右相加，要求行数相等。
theta_best = np.linalg.inv(X_b.T.dot(X_b)).dot(X_b.T).dot(y)

#prediction
X_new = np.array([[0], [2]])
X_new_b = np.c_[np.ones((2, 1)), X_new]  # add x0 = 1 to each instance
y_predict = X_new_b.dot(theta_best)
y_predict

#plot
plt.plot(X_new, y_predict, "r-")
plt.plot(X, y, "b.")
plt.axis([0, 2, 0, 15])
plt.show()

import numpy as np
import statsmodels.api as sm
import matplotlib.pyplot as plt
##################Statstics Summary###########################

reg = smf.ols('mpg ~ cylinders + displacement + horsepower + weight + acceleration + year + origin', df).fit()
model_fit = reg.fit()
reg.summary(）

reg.coef_
# fitted values (need a constant term for intercept)
model_fitted_y = model_fit.fittedvalues

# model residuals
model_residuals = model_fit.resid

# normalized residuals
model_norm_residuals = model_fit.get_influence().resid_studentized_internal

# absolute squared normalized residuals
model_norm_residuals_abs_sqrt = np.sqrt(np.abs(model_norm_residuals))

# absolute residuals
model_abs_resid = np.abs(model_residuals)

# leverage, from statsmodels internals
model_leverage = model_fit.get_influence().hat_matrix_diag

# cook's distance, from statsmodels internals
model_cooks = model_fit.get_influence().cooks_distance[0]

xfit = np.linspace(df.x.min(), df.x.max(), 100)
yfit = model.predict(xfit[:, np.newaxis])
```

#### Regularization model

[https://colab.research.google.com/drive/1MnNENQS5j2otC7quOGuqWGHg7DqCXG7g](https://colab.research.google.com/drive/1MnNENQS5j2otC7quOGuqWGHg7DqCXG7g)

```python
####################regularization sklearn#########################
np.random.seed(42)
m = 20
X = 3 * np.random.rand(m, 1)
y = 1 + 0.5 * X + np.random.randn(m, 1) / 1.5
X_new = np.linspace(0, 3, 100).reshape(100, 1)

from sklearn.linear_model import Ridge
ridge_reg = Ridge(alpha=1, solver="cholesky", random_state=42)
ridge_reg.fit(X, y)
ridge_reg.predict([[1.5]])

sgd_reg = SGDRegressor(penalty="l2", max_iter=1000, tol=1e-3, random_state=42)
sgd_reg.fit(X, y.ravel())
sgd_reg.predict([[1.5]])

from sklearn.linear_model import Lasso
lasso_reg = Lasso(alpha=0.1)
lasso_reg.fit(X, y)
lasso_reg.predict([[1.5]])

from sklearn.linear_model import ElasticNet
elastic_net = ElasticNet(alpha=0.1, l1_ratio=0.5, random_state=42)
elastic_net.fit(X, y)
elastic_net.predict([[1.5]])

from sklearn.linear_model import LogisticRegression
log_reg = LogisticRegression(solver="lbfgs", random_state=42)
log_reg.fit(X, y)
```

#### CV+ grid search

[https://colab.research.google.com/drive/1gxFuyhHKM-HXF0uiqVXfKrwGCgRDmJLN](https://colab.research.google.com/drive/1gxFuyhHKM-HXF0uiqVXfKrwGCgRDmJLN)

```python

####################CV + grid search skliearn#########################

#Use 10-fold Cross Validation to get the accuracy for different model

model_names = ['Logistic Regression', 'KNN', 'Random Forest', 'Bayes', 'GradientBoosting']
model_list = [classifier_logistic, classifier_KNN, classifier_RF, classifier_Bayes, classifier_GradientBoosting]
count = 0

for classifier in model_list:
    cv_score = model_selection.cross_val_score(classifier, X_train, y_train, cv = 10)
    print(cv_score)
    print('Model accuracy of ' + model_names[count] + ' is ' + str(cv_score.mean()))
    count += 1

#Loss/cost function --> (wx + b - y) ^2 + ƛ * |w| --> ƛ is a hyperparameter
from sklearn.model_selection import GridSearchCV
# helper function for printing out grid search results 

def print_grid_search_metrics(gs):
    print ('Best score: ' + str(gs.best_score_))
    print ('Best parameters set:')
    best_parameters = gs.best_params_
    for param_name in sorted(best_parameters.keys()):
        print(param_name + ':' + str(best_parameters[param_name]))

```

### Sampling/Bootstrap

[https://www.notion.so/yangnyc/Google-interview-solution-fe08edcd81d94e78804b5e6518ddd291](https://www.notion.so/yangnyc/Google-interview-solution-fe08edcd81d94e78804b5e6518ddd291)

#### Sample Normal：np.random.normal和plt.hist

```python
#####################Linear ########################
#Write a function to generate N samples from a normal distribution and plot the histogram.

import numpy as np
import matplotlib.pyplot as plt

data = np.random.normal(loc = 170, scale = 10, size = 250)

plt.hist(data, bins = 25, density = True, alpha = 0.6, color = 'b')
plt.show()
# sigma * np.random.randn(...) + mu 
# np.random.normal(loc= mu, scale= sigma, ...)
```

#### Bootstrap/Median/Standard Error/CI

```python
#bootstrap

# step 0: create a population distribution of 100 random numbers from 0 to 200
import numpy as np 
np.random.seed(123)
pop = np.random.randint(200, size = 100)

# step 1: take a random sample of size 10
np.random.seed(13)
sample_1 = np.random.choice(pop, 10)
sample_1

# step 2: what is the median of this sample (sample_1)?

def median_value(some):
	n = len(some)
	some.sort()
	if n % 2 ==0:
		median1 = some[n//2]
		median2 = some[n//2 - 1]
		median = (median1 + median2)/2
	else:
		median = some[n//2]
	return median

median_value(sample_1)

# step 3: repreatedly sample from the sample (sample_1) with replacement, 
# aka. bootstrap

boot_sample_medians = []
for i in range(10000):
	boot_sample = np.random.choice(sample_1, replace = True, size = 10)

	boot_median = median_value(boot_sample)
	
	boot_sample_medians.append(boot_median) #产生很多个sample的bootstrap
 

# step 4: stand error and confidence interval

# std
np.std(boot_sample_medians)

# the average value of repeated samples' median values

sum(boot_sample_medians)/len(boot_sample_median)

# C.I.
# wide CI for small sample sizes, b/c of limited sampling possibilities and large variation

boot_median_CI = np.percentile(boot_sample_medians, [2.5, 97.5])
boot_median_CI

```

#### Important Sampling：第一步st.norm.pdf(p(x)/q(x))；第二步k；第三步z是normal\_q；第三步u是uniform(0,k\*q(z))；第四步u≤p(z)

```python
#important sampling
import numpy as np 
import scipy.stats as st
import seaborn as sns
import matplotlib.pyplot

sns.set()

def p(x):
	return st.norm.pdf(x, loc = 30, scale = 10) + st.norm.pdf(x, loc = 80, scale = 20)

def q(x):
	return st.norm.pdf(x, loc = 50, scale = 30)

x = np.arange(-50, 151)
k = max(p(x)/ q(x)) #你找出那个最大的q来帮助你

def rejection_sampling(iter = 1000):
	sample = []
	for i in range(iter):
		z = np.random.normal(50, 30)
		u = np.random.uniform(0, k * q(z))
		if u <= p(z):
			samples.append(z)
	
return np.array(samples)

if __name__ == '__main__':
	plt.plot(x, p(x))
	plt.plot(x, k*q(x))
	plt.show()
	s = rejection_sampling(iter = 10000)
	sns.distplot(s)
```

#### Inverse Sampling

{% embed url="https://towardsdatascience.com/generate-random-variable-using-inverse-transform-method-in-python-8e5392f170a3" %}

<figure><img src="../.gitbook/assets/Screen Shot 2021-10-12 at 10.08.52 AM.png" alt="" width="375"><figcaption></figcaption></figure>



```python
### Generate exponential distributed random variables given the mean 
### and number of random variables
def exponential_inverse_trans(n=1,mean=1):
    U=uniform.rvs(size=n)
    X=-mean*np.log(1-U)
    actual=expon.rvs(size=n,scale=mean)
    
    plt.figure(figsize=(12,9))
    plt.hist(X, bins=50, alpha=0.5, label="Generated r.v.")
    plt.hist(actual, bins=50, alpha=0.5, label="Actual r.v.")
    plt.title("Generated vs Actual %i Exponential Random Variables" %n)
    plt.legend()
    plt.show()
    return X

### Generate arbitary discrete distributed random variables given 
### the probability vector
def discrete_inverse_trans(prob_vec):
    U=uniform.rvs(size=1)
    if U<=prob_vec[0]:
        return 1
    else:
        for i in range(1,len(prob_vec)+1):
            if sum(prob_vec[0:i])<U and sum(prob_vec[0:i+1])>U:
                return i+1

def discrete_samples(prob_vec,n=1):
    sample=[]
    for i in range(0,n):
        sample.append(discrete_inverse_trans(prob_vec))
    return np.array(sample)

def discrete_simulate(prob_vec,numbers,n=1):
    sample_disc=discrete_samples(prob_vec,n)
    unique, counts=np.unique(sample_disc,return_counts=True)
    
    fig=plt.figure()
    ax=fig.add_axes([0,0,1,1])
    prob=counts/n
    ax.bar(numbers,prob)
    ax.set_title("Simulation of Generating %i Discrete Random Variables" %n)
    plt.show()
    
    data={'X':unique,'Number of samples':counts,'Empirical Probability':prob,'Actual Probability':prob_vec}
    df=pd.DataFrame(data=data)
    return df
```

#### Shuffling algorithm(从后往前，random.randint(0,i)\&array\[i]↔array\[random\_number])

```python
def shuffle_deck(array):
	length = len(array)
	for i in range(length - 1, -1, -1): #从后往前一直走
		random_number = random.randint(0, i)  # 从之前里面选择一个出来
		array[i], array[random_number] = array[random_number], array[i]
	return array

#time O(n)
#space O(1)

# similar problems:
	# select random k elements in the size n array
	# get a k-permutation of the array of size n
```

#### Reservoir Sampling(让前面的random.randint(0, self.count-1))

```python
# how to do sampling for an unlimited data flow and we are required to return one random number among all numbers read so far, 
# such that the probability of returning any element read so far 1/n.

class Generator: #这你就是random你之前的就好了嘛
	def __init__(self):
		self.sample = 0
		self.count = 0 # the counter of elements read so far
	def read(self, val):
		self.count += 1 # current element is the count-the element
		r = random.randint(0, self.count -1) # randomly generate number from 0 to count (exclusive) [0, count-1];
		if r == 0:
			self.sample = val # the probability of choosing (count-1)- the element as the final solution is 1/count;

# assuming the number of items to select, k, is smaller than the size of the source array S
class Generator:
	def __init__(self):
		self.sample = []
		self.count = 0 # the counter of elements read so far
		self.k = k
	def read(self, val):
		self.count += 1
		if sel.fcount <= k:
			self.sample.append(val)
		else: 
			r = random.randint(0, self.count - 1) #randomly generate a number from 0 to count (exclusive) [0, count-1];
			if r < k:
				self.sample[r] = val
	

# what if we ask you to return a random largest number's index
# 找之前的最大的那个

class Generator:
	def __init__(self):
		self.max_value = float('-inf')
		self.index = -1
		self.sample = 0
		self.count = 0

	def read(self, val):
		self.index += 1
		if val > self.max_value:
			self.count = 1
			self.sample = self.index
			self.max_value = val
		elif val == self.max_val: #如果你的不是第一个，你就加计数
			self.count += 1
			r = random.randint(0, self.count -1)
			if r == 0:
				self.sample = self.index
```

#### Randomization(5\*random5()+5&大于21重新random25())

```python
# a) How to design a random number generator random(7), with random(5)

def random25():
	return 5 * random5() + random5()

def random7():
	num = random25()
	while num > 20:
		num = random25()
	return num % 7

##############################

# b) how to design a random number gnerator Random(1,000,000) with Random(2)

def rand(x):
	count = 0
	cur = x
	# get how many digits we need to have   你这里找的是我需要有多少个2相乘
	while cur > 0:
		cur = cur // 2
		count += 1
	# try to generate random number
	while True:
		sum = 0
		for i in range(count):
			# add to the sum every time we generate a new digit
			sum = sum * 2 + rand2()
		if sum < x:
			return sum

# time O(logx)
# space O(1)

##############################

# c) example: given randm(could generate 0 ~ m-1 with equal probability)
# write a function to create randx(could generate 0 ~ x-1 with equal probability)

# method
# 1. First to check how many digits we have
# 2. Generate the random number with count digits, check if it is smaller than x, 
   # if it is smaller, we just return the number, else, do it again.

def randm(m):
	return random.randint(0, m-1)

def rand(x, m):
	count = 0
	cur = x
	# get how many digits we need to have
	while cur > 0:
		cur = cur // m
		count += 1
	# try to generate random number
	while True:
		sum = 0
		for i in range(count):
		# add to the sum every time we generate a new digit
			sum = sum * m + randm(m)
		if sum < x:
			return sum

# time O(logx)
# space O(1)
```

### Gradient Method

说白了就是你有n个sample，分别分几次使用，反正每次都用在降低原来的点上，你的gradient没变，只是每次realize出来变了

$$x_{new} = x_{old} -\eta_i \nabla f(x)$$

[https://www.notion.so/yangnyc/HandsOnML-Chapter4-e5d0e68590e149b9af58dbfc0e4cfaaf](https://www.notion.so/yangnyc/HandsOnML-Chapter4-e5d0e68590e149b9af58dbfc0e4cfaaf)

#### Batch/Gradient Method

```python
def batch_gradient_descent():
    n_iterations = 1000
    learning_rate = 0.05
    thetas = np.random.randn(2, 1) #第一个点，2维
    thetas_path = [thetas]
    for i in range(n_iterations):
        gradients = 2*X_b.T.dot(X_b.dot(thetas) - y)/m #注意dot的使用
        thetas = thetas - learning_rate*gradients
        thetas_path.append(thetas)

    return thetas_path

```

#### Stochastic Gradient Method

```python
def learning_schedule(t, t0, t1):
    return t0/(t+t1)

def stochastic_gradient_descent():
    n_epochs = 50
    t0, t1 = 5, 50
    thetas = np.random.randn(2, 1)
    thetas_path = [thetas]
    for epoch in range(n_epochs):
        for i in range(m): #相当于你每一次的iter，你有m个点，你思考这m个点怎么用？gradient是一次，stochastic是m次里面的iterta？然后minibatch是每次放入一小堆
            random_index = np.random.randint(m)
            xi = X_b[random_index:random_index+1]   # 你相当于只取这个方向的x_i（错！！），是sample！！！每次只取一个
	            yi = y[random_index:random_index+1]   # 你相当于只取这个方向的y_i（错！！），是sample！！！每次只取一个
	          gradients = 2*xi.T.dot(xi.dot(thetas) - yi)     # 所以这里只除以1，你相当于选择m次，每次随意random来选方向
            eta = learning_schedule(epoch*m + i, t0, t1)      # t0/(t+t1)= t0/((epoch*m+i)+t1)这是什么。。。
            thetas = thetas - eta*gradients
            thetas_path.append(thetas)

    return thetas_path
```

#### MiniBatch Gradient Method

```python

def mini_batch_gradient_descent():
    n_iterations = 50
    minibatch_size = 20
    t0, t1 = 200, 1000
    thetas = np.random.randn(2, 1)
    thetas_path = [thetas]
    t = 0
    for epoch in range(n_iterations):
        shuffled_indices = np.random.permutation(m) #只是indices打乱
        X_b_shuffled = X_b[shuffled_indices]
        y_shuffled = y[shuffled_indices]
        for i in range(0, m, minibatch_size): #你这里又加了一个minibatch_size，而且是每次取这么多个
            t += 1
            xi = X_b_shuffled[i:i+minibatch_size] # 你相当于只取这个方向的x_i，选minibatch_size连续的方向（错）！是取batch个
            yi = y_shuffled[i:i+minibatch_size]
            gradients = 2*xi.T.dot(xi.dot(thetas) - yi)/minibatch_size #所以这里除以minibatch——s
            eta = learning_schedule(t, t0, t1) #你在调整learning scedule，一个逐渐减少的量
            thetas = thetas - eta*gradients
            thetas_path.append(thetas)

    return thetas_path
```

### AB testing

[https://colab.research.google.com/drive/1Fza8JhK1QbWEpfD0nOcmrPEZJ\_Dn6TXI?authuser=1#scrollTo=uzyThp5zyP7M](https://colab.research.google.com/drive/1Fza8JhK1QbWEpfD0nOcmrPEZJ\_Dn6TXI?authuser=1#scrollTo=uzyThp5zyP7M)

#### Generate 100000 dice rolling results

```python
import numpy as np

# this is the population
random_data = np.random.randint(1, 7, 100000)
print(random_data.mean())
print(random_data.std())

print(random_data[0:100])

sample1 = []
for i in range(0, 20):
    sample1.append(random_data[int(np.random.random())* len(random_data)])

print(sample1)

np.mean(sample1)

np.std(sample1)
```

#### CLT Central Limit Theorem

```python
# sample mean/std bootstrap

samples = []
samples_mean = []
samples_std = []

for i in range(0, 1000): #我一共需要1000来帮助我做图像
    sample = []
    for j in range(0, 50): #这里是sample出50个然后给这50个取平均
        sample.append(random_data[int(np.random.random()* len(random_data))])
    sample_np = np.array(sample)  #这是一串sample，sample的sample
    samples_mean.append(sample_np.mean())
    samples_std.append(sample_np.std())
    samples.append(sample_np)

samples_mean_np = np.array(samples_mean)
samples_std_np = np.array(samples_std)
print(samples_mean_np)

import matplotlib.pyplot as plt
%matplotlib inline
plt.rcParams.update({'figure.figsize':(7,5), 'figure.dpi':100})

# Plot Histogram on x
#x = np.random.normal(size = 1000)
plt.hist(samples_mean_np, bins=20)
plt.gca().set(title='Frequency Histogram', ylabel='Frequency');
```

#### How to calculate HT as an Algorithm(norm.cdf)

```python
from scipy.stats import norm
norm.cdf(-0.632) #这个就是直接的答案？

norm.cdf(-1.18)
norm.cdf(-3.6)
```

#### Calculate the sample size(zt\_ind\_solve\_power, proportion\_effectsize)

```python
from statsmodels.stats.power import zt_ind_solve_power
from statsmodels.stats.proportion import proportion_effectsize as es

#从0.1 提高到0.12的转化率？alpha = 0.5， power = 0.8， alternative = two_size
simple_size = zt_ind_solve_power(effect_size = es(prop1 = 0.1, prop2 = 0.12), alpha = 0.5, power = 0.8, alternative = 'two-sided')
```

#### Test for Independence(U, p, dof, expected = chi2\_contingency(table, correction = False))

print(U) #卡方值

1. Two discrete:：Simpson paradox
2. Two Continuous variables:：look at their correlation
3. One Continuous variable and one discrete: look at the test statistics $$D=\sup \|\hat{F}_1(x)-\hat{F}_2(x)\|$$

```python
# chi-squared test with similar proportions
from scipy.stats import chi2_contingency
from scipy.stats import chi2

#contingency table

table = [[90, 165, 34],[84,  307, 65]]

print(table)

U, p, dof, expected = chi2_contingency(table, correction = False)
print(U) #卡方值
print(p) #p值
print('dof=%d' % dof) #degree of freedom
print(expected) #与原数据数组同维度的对应理论值

#interpret p-value
alpha = 0.05
print('significance=%.3f, p=%.3f' % (alpha, p))

if p <= alpha:
    print('Dependent (reject H0)')
else:
    print('Independent (fail to reject H_0)')
```

#### p-value:

* 是一个数字，越小，反应出现的情况越极端，基于现有的observation，在null hypothesis下
  * court，innocent，knife on the crime scene

#### statistical significance:

* a decision, which concerning a value stated in the null hypothesis

#### hypothesis：

* claim/population/parameter
* $$H_0$$ claim reflect default ，ex no relation/no difference
* $$H_1$$ claim about population/hypothesis H\_0 false

#### significance level $$\alpha$$:

* probability, reject $$H_0$$ under $$H_0$$ is true

#### type I error（冤狱）:

* when $$H_0$$ is true, but rejected
* {p-value | H\_0 is true} \~ uniform(0,1)
* type I error rate = Pr(reject H\_0| H\_0 is true) = Pr(p-value < significance level| H\_0 is true)= significance level

#### type II error（漏网）:

* when H\_1 is true, but rejected
* $$\beta = Pr(not \ reject \ H_0| H_1 \ is \ true) = 1- Pr( reject \ H_0| H_1 \ is \ true)= 1- power$$

#### power(火眼金睛):

* the probability of rejecting H\_0, when H\_1 is true
* $power = 1-\beta$
