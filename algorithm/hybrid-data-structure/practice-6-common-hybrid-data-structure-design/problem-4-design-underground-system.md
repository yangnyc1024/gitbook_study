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
* **CheckIn能给我们什么信息？**
  * 哪个人（一个人）， startStation
  * 哪个人（一个人）， endStation
* **零散：不是从一个API的所有数据就可以直接计算你想得到的结果**
  * getAverageTime要想有合法数据，至少得有一个人完成了进站
* **汇总成什么信息**
  * getAveragetime ==》 进站 ->出站 + 总人数 +总时间
* **问题1:id 干嘛？真的没有用吗？**
  * 你出站检票的时候，是不是得知道这个人<mark style="color:blue;">用了多久</mark>，这个人是<mark style="color:blue;">从哪站到了哪站</mark>
  * 如何从进站的信息中提取出，这个人的入站口和时间
  * 沟通的作用

#### Detail Logics

**Step 1: 根据操作API--》 数据结构选择**

* <mark style="color:blue;">API 1: getAverageTime(string, startStation, string endStation)</mark>
  * <进站 --》 出站 + 总人数 + 总时间>
  * inser + look up
  * Map\<String, Map\<String, <mark style="color:blue;">Pair<总时间，总人数></mark>>> map
  * **问题2:出站口当key可以吗？**ok
  * **问题3:内层的value需要记录一个pair可以只记录一个吗？**不行，每个元素都是求result必须的
* <mark style="color:blue;">API 2: CheckIn or CheckOut?</mark>
  * CheckIn能给我们什么信息？
    * 哪个人（一个人）， startStation ， 入站时间
  * CheckOut能给我们什么信息？
    * 哪个人（一个人），endStation，出战时间
  * 我要是想要更新上一步map，我能在check out更新，在check out 更新的时候
    * look up进站的信息by id
  * 进站的信息是必须记录的，但是出站的信息启示可以汇总到总的结果map里面
  * Map\<Integer, 进站的信息> ==》 Map\<Integer, Map\<String, Integer>> checkInMap
    * Map\<ID, Map\<start station, time>>

**Step 2: 模拟运行整个程序**

* Map\<String, Map\<String, <mark style="color:blue;">Pair<总时间，总人数></mark>>> map
* Map\<Integer, 进站的信息> ==》 Map\<Integer, Map\<String, Integer>> checkInMap
* <mark style="color:blue;">void checkIn(int id, string stationName, int t)</mark>
  * **case 1: 没有**
    * 直接创建一条记录\<id,\<startStation, time>>
  * **case 2: 有**
    * id： check in station 存在不存在
    * **case 2.1 存在**
      * update check in time
      * 如果这人没有checkOut==> **检查一下时间 -->不知道逃没逃**
    * **case 2.2 不存在**
      * 直接创建一条记录\<id, \<startStation, time>> ==> **update Time**
* <mark style="color:blue;">void checkOut(int id, string stationName, int t)</mark>
  * <mark style="color:blue;">**case 1: 存在**</mark>
    * <mark style="color:blue;">根据从checkIn的map取出Map\<startStation, time></mark>
    * 根据当前的时间和取出来的上车时间，算这个人的**用时**
    * 人数就是自己一个人，算一个人头
    * resultMap
      * 先看看resultMap里面有没有这个人的start station
      * **case 1.1有：**
        * 再看看这个上车的车站有没有一个一一映射到这个出站的station
        * **case 1.1.1 有**
          * 把时间累加在原来的总时间上
          * 通过的总人数 + 1
        * **case 1.1.2 没有**
          * create a new record
        * \<startStation --> endCity, 总时间，1>
      * **case 1.2没有：**
        * create a new record
        * \<startCity --> endCity, 总时间， 1>
  * **case 2:不存在**
    * new API 补票：\<startStation, Time>



````java
// Some code


```java
class UndergroundSystem {
    class Pair {
        int count;
        long totalTime;
        public Pair(int c, long t) {
            this.count = c;
            this.totalTime = t;
        }
    }
    Map<Integer, Map<String, Integer>> checkInMap;
    Map<String, Map<String, Pair>> resultMap;
    public UndergroundSystem() {
        this.checkInMap = new HashMap<>();
        this.resultMap = new HashMap<>();
    }
    
    public void checkIn(int id, String stationName, int t) {
        this.checkInMap.putIfAbsent(id, new HashMap<String, Integer>());
        this.checkInMap.get(id).put(stationName, t);
    }
    
    public void checkOut(int id, String stationName, int t) {
        Map<String, Integer> checkInInfo = this.checkInMap.get(id);
        String startStation = null;
        int startTime = 0;
        for (String key: checkInInfo.keySet()) {
            startStation = key;
            startTime = checkInInfo.get(key);
            break;
        }
        checkInMap.remove(id);
        resultMap.putIfAbsent(startStation, new HashMap<String, Pair>());
        Map<String, Pair> checkOutInfo = resultMap.get(startStation);

        if (checkOutInfo.containsKey(stationName)) {
            Pair current = checkOutInfo.get(stationName);
            current.count++;
            current.totalTime += (t- startTime);
            checkOutInfo.put(stationName, current);
        }else{
            checkOutInfo.put(stationName, new Pair(1, t- startTime));
        }
    }
    
    public double getAverageTime(String startStation, String endStation) {
        if (!resultMap.containsKey(startStation)) {
            return -1.0;
        }
        Map<String, Pair> checkOutInfo = resultMap.get(startStation);
        Pair result = checkOutInfo.get(endStation);

        if (result == null) {
            return -1.0;
        } else {
            return (double)(result.totalTime)/(result.count);
        } 
    }
}
```
````
