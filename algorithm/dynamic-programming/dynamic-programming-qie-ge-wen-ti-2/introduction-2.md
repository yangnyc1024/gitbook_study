# Introduction 2

NK问题

* 把一个长度为N的item，分成k份，使得某个特征值最值化
* 本质相当于对长度单位进行升级维度，对于同样长度的问题，所剩余的刀数不同，问题答案是不同的

DP定义的时候

* 第一个维度，给份数，第二个维度，给长度

dp\[k]\[n] represent partition n length item to k parts, max/ min/ boolean ...特征值



Base case

* 第一种是不用切 = 不切 = 1份 ==》 dp\[1]\[any] = 特征值of whole array
* 第二种是没得可切 ==〉 k > n, 没法切，要想分成k份，长度至少得有k把

Induction Rule

* dp\[k]\[i] ==>看所有可能的切点j
* dp\[k -1]\[j] 左大段
* 切下来的一份 右小段

