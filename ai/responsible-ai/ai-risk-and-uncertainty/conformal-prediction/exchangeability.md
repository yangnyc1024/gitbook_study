# Exchangeability

## Exchangeable random variables







## Prediction without covariates

#### Lemma 1

Suppose $$Z_1, \cdots Z_n$$ are exchangeable random variables. For any $$\alpha \in \{0, 1\}$$, $$P[Z_n \leq \hat{Q}_n(\alpha)] \geq \alpha$$

Moreover, if $$Z_1, \cdots Z_{n}$$ are a.s distinct, $$P[Z_{n} \leq \hat{Q}_{n+1}(\alpha)] \leq \alpha + \frac{1}{n}$$

* key proof: using the uniform distribution or these order statistics?

**Lemma 2**

Suppose $$Z_1, \cdots Z_{n+1}$$ are exchangeable random variables. For any $$\alpha \in \{0, 1\}$$, define $$\alpha_n$$ as $$\alpha_n = (1 + \frac{1}{n})\alpha$$. Then, $$P[Z_{n+1} \leq \hat{Q}_{n+1}(\alpha_n)] \geq \alpha$$

Moreover, if $$Z_1, \cdots Z_{n+1}$$ are a.s distinct, $$P[Z_{n+1} \leq \hat{Q}_{n+1}(\alpha_n)] \leq \alpha + \frac{1}{n}$$.

* Key of the proof:
  * use lemma 1 and change n points to (n+1) points of these order statistics
  * and you cannot jump for two points since you only added one point into the empirical distribution

## One-sided prediction interval without covariates



