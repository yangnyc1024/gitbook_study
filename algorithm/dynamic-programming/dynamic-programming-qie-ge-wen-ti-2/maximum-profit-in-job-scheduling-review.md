# Maximum Profit in Job Scheduling Review

从切割角度思考，dp定义的维度， 时间维度vs Job角度

view 1:时间角度



定义：

* dp\[i] represents the maximum point you could get starting from time point i ==> i is a time point

Induction Rule:

* Time length = maxEndingTime - minStartingTime
* dp\[i] = Math.max(dp\[i], temp.profit + dp\[calculated by temp.end])







view 2:job维度

定义：

* dp\[i] represents the maximum point you could get using all the jobs ending at index i

Induction Rule:

* dp\[i] = Max(dp\[i - 1],  ith job profit + dp\[maximum j such that jth job is not overlapping with ith job])
