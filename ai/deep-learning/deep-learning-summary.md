# Deep Learning Summary

## Deep Learning

### motivation of deep learning

* limitation of traditional machine learning
  * feature engineering
  * high dimensional data
* why deep learning
  * feature learning
  * big data
  * computation power

## Tutorial on Pytorch

### Tensor

### Autograd

* 基本流程？
  * 搭建计算图
  * 求损失函数forward（如何算？）
  * 计算损失函数对模型参数的倒数backward（如何算？）
  * 用梯度下降法更新参数gradient descen

### NN module

## Two neural network

### Perceptron and Activation function

* Perceptron（感知机器）![](https://api2.mubu.com/v3/document\_image/92167e8d-a085-4503-a2fe-fa8674749027-12267179.jpg)
* one hidden layer（两层感知机）![](https://api2.mubu.com/v3/document\_image/0fea87a7-e29e-452b-a491-701d409a4b4b-12267179.jpg)
* activation functions（激活函数）
  * sigmoid
    * 性质？
    * 什么时候使用
  * Tanh
  * Relu
    * 性质
    * 什么时候使用
* 输出层结构（概率&结果）
  * softmax

### NN network 2

#### Regularizations

* dropout

#### Initialization

* pitfall/small random numbers/calibrating the variance with 1/sqrt(n)

#### Batch normalization

### Backpropagation

#### Concept

#### Forward propagation/链式法则

#### Backpropagation

#### Backpropagation for two layer neural network





## Convolutional Neural Network

### Convolution

#### Why convolution?if fully connected?

* connect neuron in the hidden layer to all neurons in the input layer
* no spatial information
* many parameter!

#### Convolution Kernel

* 就全部点乘（相当于weight）![](https://api2.mubu.com/v3/document\_image/0a49e702-9666-40aa-9079-2e51a59a95ad-12267179.jpg)
* 卷积模板/滤波矩阵/kernel/filter
  * Identity map
  * 平滑均值滤波
  * 边缘检测卷积核

#### Convolution operation

* Padding填充
  * n原来图形尺寸，f是filter长宽
  * $$p=\frac{(f-1)}{2}$$
* Stride步长
  * s步长
  * $$n * n \rightarrow[\frac{(n+2p-f)}{s}+1]*[\frac{(n+2p-f)}{s}+1]$$ &#x20;

### Layer

#### Convolution Layer

* What is？
* 局部连接
* 空间排列
* 参数共享

#### Pooling Layer

* What is？

#### Fully Connected Layer

#### Non-linearity/ReLU

#### Batch Normalization

### Important CNN Architectures

* Lenet（理解/应用）
* Alexnet(理解/应用)
* VGG（应用）
* Googlenet(inception)(应用)
* REsnet(应用)

### Transfer Learning

* Transfer Learning vs traditional ML
  * ![](https://api2.mubu.com/v3/document\_image/3788f9d5-ebfd-4138-924e-27f2593218b7-12267179.jpg)
* Transfer Learning idea
  * ![](https://api2.mubu.com/v3/document\_image/216e9795-6587-4910-8713-d0978b724e23-12267179.jpg)
* Off-the-shell
  * ![](https://api2.mubu.com/v3/document\_image/7bf249b9-0e84-43c1-980d-14c5c50665d8-12267179.jpg)
* when to us
  * CNN as fixed feature extractor
    * use cnn features + other classifier such as SVM, softmax classifier
    * fine-tuninng the CNN
    * pretrained models
    * When?
      * small and similar
      * large and similar
      * small but very different
      * large but very different

## Recurrent Neural Network

### When？

* 主要解决样本序列为序列的建模/每个元素不独立相互依赖
* variable-sized

### 原理

* recurrence formula$$h_t = f_W(h_{t-1}, x_t)$$
* design to solve what problem?![](https://api2.mubu.com/v3/document\_image/422b590c-2b45-4c45-8df1-f33fa7bd26a5-12267179.jpg)
  * one to one: vanilla CNN NN
  * one to many: Image captioning, decoder part of translation model(seq2seq)
  * many to one: sentiment analysis of text, encoder part of translation model
  * many to many: translation. per-frame video classification, sequence tagging
* Backpropagation through time(BPTT)
  * Truncated Backpropagation through time

### Long-short term memory(LSTM)

#### Motivation/What does LSTM do?

* vanilla RNN are not very good at capturing long-term dependency

#### What does LSTM look like?

* Forget gate
* New memory cell gate
* Update old memory cell state
* Output gate

#### Why LSTM works?

* Gradient flow
* Do LSTM solve the vanishing gradient problem?

#### More powerful: Transformer(replace RNN, LSTM)

* Key advantage of Transformers
  * LSTM still good when?

#### Important RNN models

* Seq2seq
* Bidirectional RNN/LSTM

## DL Application

### 什么是embeddings和word2vec

### word2vec模型

* 分成两个部分
* fake task
* skip-gram and CBOW(continuous bag of words)
* 模型细节
* word2vec模型训练
* word2vec application
  * 万物皆可embedding

### Regularization in Deep Learning

* dropout(usually in dense layer)
* data augmentation(CNN)
* model emsemble
* early stopping
* batch norm

### Deep Learning Applications

#### 在那？

* Supervised Learning: CNN/RNN
* Unsupervised Learning: GAN
* Reinforcement Learning: DQN/A3C/PPO\


#### framework 如何判断一个新的？

* 重要组成部分![](https://api2.mubu.com/v3/document\_image/b671133e-0dae-4d09-bb4d-d79ae7ea65b4-12267179.jpg)\

* recommendation
  * input/output
    * structured data/ranking score
  * Architecture:
    * wide/deep/wide\&deep network
  * Loss
    * sigmoid/binary\_crossentropy
* 图像：
  * input/output
    * 图像/spectrogram/基于标签
  * Architecture:
    * pytorch观察模型结构
  * Loss
    * 多分类cross-entropy
* BERT语言
  * input/output
    * 一对句子15%token（mask）
  * Architecture:
    * embedding：基于双向注意力机制的多层encoder网络（tranasformer）
  * Loss
    * cross-entropy

#### Deployment

* training 策略
* inference策略
  * pruning
  * quantization
* deep learning platform
* why deep learning? amount of data

### 调参
