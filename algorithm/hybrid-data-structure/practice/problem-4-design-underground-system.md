# Problem 4 Design Underground System

#### Step 1：明确题目让你做什么，你需要干啥

* 这道题让我们<mark style="color:blue;">design 一个数据结构</mark>，这个数据结构有几个api



#### Step 2：明确API

* void checkIn(int id, string stationName, int t)
* void checkOut(int id, string stationName, int t)
* double getAverageTime(string startStation, string endStation)
* getAverageTime = 所有通过start和end的总时间/所有人的总人数



#### High Level

* 需要知道，所有通过start和end的总时间 &总人数
* 可以全部记下来？&#x20;
* 从哪里来？checkIn and checkOut
