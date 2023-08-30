# Question 9 Search Unknown Value



## Method 1 Brute Force



## Method 2这题目是sorted==》 binary search



## Method 2.1 只有右边不断扩展



## Method 2.2 左边也跟着跳

```java
int search(UnboundedArray arr, int target) {
    if (arr == null || arr.get(0) == null) {
        return -1;
    }
    int left = 0;
    int right = 1;
    while (array.get(index) != null && array.get(index) < target) {
        left = right;
        right *= 2;
    } 
    // search range [left, right]
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr.get(mid) == target) {
            return mid;
        }
        else if (arr.get(mid) < target) {
            left = mid + 1;
        }
        else {
            right = mid - 1;
        }
    }
    return -1;
}
```
