# Question 6 Closest Element to Target

```java
int closest(int[] nums, int target) {
    // corner case
    int left = 0;
    int right = nums.length - 1;
    while (left < right - 1) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            return mid;
        }
        else if (nums[mid] < target) {
            left = mid;
        }
        else {
            right = mid;
        }
    }
    if (Math.abs(array[left] < target) <= Math.abs(array[right] - target)) {
        return right;
    }
}
```
