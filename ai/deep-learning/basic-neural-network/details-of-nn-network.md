# Details of NN network

## Regularization

**Dropout** is an extremely effective, simple and recently introduced regularization technique by Srivastava et al. in **Dropout: A Simple Way to Prevent Neural Networks from Overfitting** (pdf) that complements the other methods (L1, L2, maxnorm).&#x20;

* While training, dropout is implemented by only keeping a neuron active with some probability ( p ) (a hyperparameter), or setting it to zero otherwise.

Figure taken from the **Dropout** paper that illustrates the idea. During training, Dropout can be interpreted as **sampling a Neural Network within the full Neural Network**} and only updating the parameters of the sampled network based on the input data.&#x20;

* (However, the exponential number of possible sampled networks are **not independent** because they share the parameters.)&#x20;
* During testing, there is no dropout applied, with the interpretation of evaluating an averaged prediction across the exponentially-sized ensemble of all sub-networks (more about ensembles in the next section).

## Initialization

**Pitfall: all zero initialization**

Let's start with what we should not do. Note that we do not know what the final value of every weight should be in the trained network, but with proper data normalization it is reasonable to assume that approximately half of the weights will be positive and half of them will be negative. A reasonable-sounding idea then might be to set all the initial weights to zero, which we expect to be the "best guess" in expectation.

**Small random numbers**

The idea is that the neurons are all random and unique in the beginning, so they will compute distinct updates and integrate themselves as diverse parts of the full network. The implementation for one weight matrix might look like: $$W = 0.01 \times \text{np.random.randn}(D,H)$$ where **randn** samples from a zero mean, unit standard deviation Gaussian. With this formulation, every neuron's weight vector is initialized as a random vector sampled from a multi-dimensional Gaussian, so the neurons point in random directions in the input space. It is also possible to use small numbers drawn from a uniform distribution, but this seems to have relatively little impact on the final performance in practice.

**Calibrating the variances with** $$1/\sqrt{n}$$

That is, the recommended heuristic is to initialize each neuron's weight vector as: $$w = \frac{\text{np.random.randn}(n)}{\sqrt{n}}$$ where $$n$$ is the number of its inputs. This ensures that all neurons in the network initially have approximately the same output distribution and empirically improves the rate of convergence.

## Batch normalization

Motivation: Speed up the process of training deep neural networks by reducing **Internal Covariate shift**



<figure><img src="../../.gitbook/assets/Screenshot 2024-09-18 at 7.29.23 PM.png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2024-09-18 at 7.29.48 PM.png" alt="" width="375"><figcaption></figcaption></figure>

Reference: [https://zhuanlan.zhihu.com/p/26138673](https://zhuanlan.zhihu.com/p/26138673)

## Backpropagation

你的目的是为了要求最小值

## Backpropagation Details

### forward propagation

### backward propagation

## Gradient vanish VS gradient explode









Reference

* [http://galaxy.agh.edu.pl/\~vlsi/AI/backp\_t\_en/backprop.html](http://galaxy.agh.edu.pl/\~vlsi/AI/backp\_t\_en/backprop.html)
* 课程

