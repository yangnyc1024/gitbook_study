# Question 1b 2 Sum II

clarification of problems

* sorted or unsorted&#x20;
* duplicate?



<mark style="color:red;">**我们其实是for each j，**</mark>

* <mark style="color:red;">**去找smallest i， s.t. array\[i] >= target - array\[j]**</mark>

####

## Sorted array, no duplicate

#### Method 1 Brute Force

check all pair (i, j) see if array\[i] + array\[j] = target



如何找，需要让pair有顺序出现

* 所以可以用i < j <mark style="color:red;">(小trick，固定大的找小的，大多数时候会比较的方便)</mark>
* 所以相当于在找array\[i] == target - array\[j]
* smallest array\[i] >= target - array\[j]

option 1: binary search using sorted array

option 2: HashSet record all the elements before j

option 3: 相向而行的two pointer

```java

class Solution {
    public int twoSum(int[] numbers, int target) {
        // sanity check
        if (numbers == null) {
            return new int[]{-1, -1};
        }
        int left = 0;
        int right = numbers.length - 1;
        int count = 0
        while (left < right) {
            int sum = numbers[left] + numbers[right];
            if (sum == target) {
                count++;
                right--; // 注意这个地方，不需要去弄left
            }
            if (array[left] < target - array[right]) {
                left++; // for current right, try to find smallest array[left] >= target - array[j] but not found yet
            }
            else {
                right--; // check next right;
            }
        }
        return count;
    }
}
```

## Sorted array, duplicate not count

```java
class Solution {
    public int twoSum(int[] numbers, int target) {
        // sanity check
        if (numbers == null) {
            return new int[]{-1, -1};
        }
        int left = 0;
        int right = numbers.length - 1;
        int count = 0
        while (left < right) {
            int sum = numbers[left] + numbers[right];
            if (sum == target) {
                count++;
                //right--; // 注意这个地方，不需要去弄left
                while (left < right && array[right] == array[right- 1]) {
                    right--;
                }
                right--;
            }
            if (array[left] < target - array[right]) {
                //left++; // for current right, try to find smallest array[left] >= target - array[j] but not found yet
                while (left < right && array[left] == array[left + 1]) {
                    left++;
                }
                left++;
            }
            else {
                //right--; // check next right;
                while (left < right && array[right] == array[right- 1]) {
                    right--;
                }
                right--;
            }
        }
        return count;
    }
}
```

## Sorted array, duplicated elements count

唯一区别，就是多count

\[1,1,2,2,2,2,2,3,3,3,3] taregt 4, return 18

```java
            if (sum == target) {
                if (array[left] == array[right]) {
                    count+ = (right - left + 1) * (right - left) / 2;
                }
                int countLeft = 0;
                int countRight = 0;
                //right--; // 注意这个地方，不需要去弄left
                while (left < right && array[right] == array[right- 1]) {
                    right--;
                    countRight++;
                }
                while (left < right && array[left] == array[left + 1]) {
                    left++;
                    countLeft++;
                }
                left++;
                right--;
                count += countLeft * countRight;
            }
```

## Unsorted array # of pairs sum to target

有多少index i such that i < j.

* 在\[0, j - 1] 有多少个元素，值是target- array\[j]
* 优化这一步，怎么做，需要用什么数据结构做，数据结果存什么？

<pre class="language-java"><code class="lang-java"><strong>int count = 0;
</strong><strong>Map&#x3C;Integer, Integer> occurrence = new HashMap&#x3C;>();
</strong><strong>for (int j = 0; j &#x3C; array.length; j++) {
</strong>    //有多少元素，值是target- array[j]
    count += occurrence.getOrDefault(target - array[j], 0);
    // put array[j] into the map
    occurrence.put(array[j], occurrence.getOrDefault(array[j], 0) + 1);
} 
</code></pre>

