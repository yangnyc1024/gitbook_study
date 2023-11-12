# Question 3 Iterator for Permutation







#### 规律

example；最小和最大的值, n = 5, k =3

* combination: min: 123前k位，max345后k位
* permutation: min: 123前k位，max543后k位的逆序



#### Method 1: Backtracking  Pre-Calculate all permutation

#### Method 2:1999+ 1= 2000

关键点：

* 第一个一定是全升序
* 最后一个一定是全降序
* bdca后半部分都是递减的人—— 》b是第一个破坏降序（可以增大）的字母—— 〉haunch鞥比他大的最小的——》cabd

观察下

* 你的下一个一定是比你大的最小的
* 这就是为什么我写1999 + 1 而不是2999



Detail Logic

Step 1:

* 找到破坏全降序的第一个字母
* 如果没有找到这样的字母，说明没有下一个

Step 2:

* 找到一个字母和这个字母交换，保证得到的是比他大的最小的
* 保证得到的是比他大的最小的：倒叙遍历看第一个大于当前字母的

Step 3：

* reverese the whole part except this digit!
* 那么为什么要reserve呢：swap 能保证后面的部分仍然是降序，所以要reverse成最小的



工具人写法：很多题目需要用到next permutation

```java
public void nextPermutation(int[] nums) {
    if (nums == null || nums.length == 0) {
        return;
    }
    int i = nums.length - 2;
    while (i >= 0 && nums[i] > nums[i+1]) {
        i--;
    }
    if (i >= 0) {
        int j = nums.length - 1;
        while (nums[j] < nums[i]) {
            j--;
        }
        swap(nums, i, j);
    }
    reverse(nums, i + 1,nums.length - 1);
}
private void swap(int[] nums, int i , int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
private void reverse(int[] nums, int i, int j) {
    while (i < j) {
        swap(nums, i++, j--);
    }
}
```









