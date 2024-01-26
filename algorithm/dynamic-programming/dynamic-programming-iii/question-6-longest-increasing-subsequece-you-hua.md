# Question 6 Longest Increasing Subsequece 优化

Method Greedy + Binary Search

```java
public int longestOfLIS(int[] array) {
    int[] lowestEnding = new int[array.length + 1];
    int lengthOfLIS =1;
    loestEnding[1] = array[0];
    for (int i = 1l i < array.length; i++) {
        int index = firstOccurrence(lowestEnding, 1, lengthOfLIS, array[i]);
        if (index == -1) {
            //开辟新天地，延续
            lowestEnding[lengthOfLIS + 1] = array[i];
            lengthOfLIS++;
        }else{
            lowestEnding[index] = array[i];
        }
    }
    return lengthOfLIS;
}
private int first Occurrence(int[] array, int left, int right, int target) {
    while (left < right - 1)  {
        int mid = left + (right - left) /2;
        if (array[mid] >= target) {
            right = mid;
        }
        else {
            left = mid + 1;
        }
    }
    if (array[left] > = target) {
        return left;
    }
    if (array[right >= target]) {
        return right;
    }
    return -1;
}
```



