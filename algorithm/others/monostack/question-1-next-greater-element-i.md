# Question 1 Next Greater Element I



### Method 1: Brute Force O(n^2)

* Step 1: 在 nums2里找到和这个数
* Step 2: 往右看，找第一个比我大的

### Method 2: Optimization

#### Analysis

* 用单调栈撸一遍，是撸nums1还是撸nums2？只能撸nums2
* 就算用单调栈撸一遍nums2了以后，只能知道，nums2里每个元素对应右边第一个比他大的是谁
  * nums2 = \[1,3,4,2], result\[3,4,-1,-1]
* &#x20;问题在于对不上元素，虽然知道了nums2里面每个元素的结果，但是不不知道nums1里每一个元素在nums2里的位置
  * Map\<Key: nums, Value: 这个元素在nums2 index> map

#### Details

* Step 1: 确认Use Case of Mono -Stack
* Step 2: 用的是什么栈：动手过个例子（2元素就够了）
* Step 3: 栈里存的是什么物理意义

#### Follow Up

* nums2.length >>>> nums1.length
  * Map------Key:每个nums2的元素，Value：右边第一个比他大的结果
* 如果记录的是index，每个人必然有index， O(n)开定了
* 如果记录的是result，每个人右边可能没有比他大的人，不一定



```java
// Some code
public int[] nextGreatElement(int[] nums1, int[] nums2) {
    Map<Integer, Integer> resultMap = new HashMap<>();
    int[] result = new int[num1.length];
    
    Deque<Integer> monoStack = new ArrayDeque<>();
    for (int i = 0; i < nums2.length; i++) {
        while (!monoStack.isEmpty() && monoStack.peekLast() < nums2[i]) {
            resultMap.put(monoStack.pollLast(), nums2[2]); // monoStack存的是nums2的element
        }
        monoStack.offerLast(nums2[i]);
    }
    for (int i = 0; i < nums1.length; i++) {
        result[i] = resultMap.getOrDefault(nums1[i], -1);
    }
    return result;
}

```
