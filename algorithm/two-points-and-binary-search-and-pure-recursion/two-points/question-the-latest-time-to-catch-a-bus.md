---
description: https://leetcode.com/problems/the-latest-time-to-catch-a-bus/description/
---

# Question The Latest Time to Catch a Bus

#### High Level && Detail Logic:

* Step 1: 我们需要知道最后赶上这辆车最后一个人到达的时间：这样我们就知道那些人能够赶上这一辆车
  * 上不了前一车的人，必然是后一辆车的candidate
* Step 2: 知道这辆车能带走多少人
  * 到目前为止一共走了多少人
  * 我们知道每辆车能带走到那个人，能知道每辆车能带走多少人以及堆积量是多少，目的是知道最后时刻的情况
* Step 3: 怎么判断最后的时刻
  * 如果最后一辆车装不满：如果没人能赶上车，或者最后一个人后面都有地方-最后时刻上车
  * 如果你要是等的话肯定上不了车，那就必须要挤下去一个人，挤掉最后一人，要夹缝里生存

#### Detail Logic

我们需要知道最后赶上这辆车最后一个人到达的时间

* bus.length \~ 10^6--->基本上说是n方时间

怎么在bus和passenger两个数组里确认每辆车最后一个能赶上的人是谁？

* Search range: \[0, passenger.length - 1]
* Search for what: last occurrence of passenger\[i] such that passenger\[i] <= curBusArrValtime



```java
public int lastestTimeCatchTheBus(int[] busDepartureTimes, int[] passengerArrivalTimes, int capacity) {
    Arrays.sort(busDepartureTimes);
    Arrays.sort(passengerArrivalTimes);
    
    int currentTotalPassengers = 0;
    int currBusCapacity = 0;
    int lowerBoundArrivalTimeIndex = -1;
    
    for (int busDepartureTime: busDepartureTimes) {
        lowerBoundArrivalTimeIndex = getLowerBound(passengerArrivalTimes, busDepartureTime);
        currBusCapacity = Math.min(capacity, lowerBoundArrivalTimeIndex - (currentTotalPassengers - 1));
        currentTOtalPassengers += currBusCapacity;
    }
    if (currBusCpacity < capacity && (lowerBoundArrivalTimeIndex == -1 || passengerArrivalTimes[lowerBoundArrivalTimeIndex] + 1 <= busDepartureTimes[busDepartureTimes.length - 1])) {
        return busDepartureTimes[busDepartureTimes.length - 1];
    }
    for (int i = currentTotalPassengers - 1; i >= 0; i--) {
        if (i > 0 && [assengerArrivalTimes[i] - 1 != passengerArrivalTimes[i -1]) {
            return passengerArrivalTimes[i] - 1;
        }
    }
    return passengerArrivalTimes[0] - 1;
}

private int getLowerBound(int[] arr, int busArriveTime) {
    int left = 0;
    int right = arr.length - 1;
    
    if (arr[left] > busArriveTime) {
        return -1;
    }
    while (left < right - 1) {
        int mid = left + (right - left) / 2;
        if (arr[mid] <= busArriveTime) {
            left = mid;
        } else {
            right = mid -1;
        }
    }
    if (arr[right] <= busArriveTime) {
        return right;
    }
    if (arr[left] <= busArriveTime) {
        return left;
    }
    return -1;
}
```
