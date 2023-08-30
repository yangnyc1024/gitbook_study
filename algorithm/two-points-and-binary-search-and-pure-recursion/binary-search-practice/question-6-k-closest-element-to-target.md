# Question 6 K Closest Element to Target

```java
public class Solution {
  public int[] kClosest(int[] array, int target, int k) {
    // Write your solution here
    if (array == null || array.length == 0) {
      return null;
    }
    if (k == 0){
      return new int[0];
    } 
    int[] result = new int[k];
    int left = closest(array, target);
    int right = left + 1;
    for (int i = 0; i < k; i++) {
      if (left < 0) {
        result[i] = array[right];
        right++;
      }
      else if (right > array.length - 1) {
        result[i] = array[left];
        left--;
      }
      else if (Math.abs(array[left] - target) <= Math.abs(array[right]- target)) {
        result[i] = array[left];
        left--;
      }
      else {
        result[i] = array[right];
        right++;
      }
    }
    return result;
  }

  public int closest(int[] array, int target) {
    // Write your solution here
    // corner case
    if (array == null || array.length == 0) {
      return -1;
    }
    int left = 0; 
    int right = array.length - 1;
    while (left < right - 1) {
      int mid = left + (right - left) / 2;
      if (array[mid] == target) {
        return mid;
      }
      else if (array[mid] < target) {
        left = mid;
      }
      else {
        right = mid;
      }
    }
    if (Math.abs(array[left] - target) < Math.abs(array[right] - target)) {
        return left;
      }
    return right;
  }
}
```
