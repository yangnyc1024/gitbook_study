# Problem 1 Classical Binary Search

Version 1

```java
public solution {

    public int binarySearch(int[] nums, int target) {
    
        // sanity check
        
        // narrow down the search area until find the result
        // get search area [left, right]
        // find [left, mid), mid, (mid, right]
        while (left <= right) {
            int mid = left + (right - left) /2;
            if (array[mid] == target) {
                return mid;
            }
            else if (array[mid] < target) {
                left = mid - 1;
            }
            else {
                right = mid + 1;
            }
        }
    }
}
```
