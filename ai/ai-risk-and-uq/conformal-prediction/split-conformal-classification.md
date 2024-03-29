# Split Conformal Classification

## The classification problem





## Uncertainty estimation via calibrated prediction sets





## Prediction sets for classification: the ideal approach





## The classification oracle& The conservative classification oracle



## Machine learning classification models







## Plug-in prediction sets will often fail





## Calibration via conformity scores



## Split-conformal classification









##







$$y \in [C] = \{1, 2, \cdots, C\}$$

$$\pi_c(x) = P[Y= c | X= x]$$

![](<../../.gitbook/assets/Screenshot 2023-06-04 at 1.50.49 PM.png>)





所以这里用到generalized conditional quantile function?





如果太多了，你就对最后一个label进行random，让probability到1-\alpha

但是会导致常常under coverage？尤其是在deep learning的时候

![](<../../.gitbook/assets/Screenshot 2023-06-04 at 1.57.58 PM.png>)







What is $$\gamma$$?

* $$\gamma$$ just the threshold you choose

What do we do in the calibration set?

* we cal the curve, and find the probability(就是左边这个玩意)，然后确保你的true label可以在里面，那么这就是你这个calibration得出来的numerical score
* 你有很多这样的probability，然后组成empirical distribution
* choose 你想要要的alpha，然后poll out这个emeprical probabiltty（有时候是1-alpha？）





