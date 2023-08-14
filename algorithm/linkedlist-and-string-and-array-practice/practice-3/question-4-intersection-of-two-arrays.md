# Question 4: Intersection of Two Arrays

```java

int[] intersection(int[] num1, int[] num2) {
    Array.sort(num1);
    Array.sort(num2);
    int i = 0;
    int j = 0;
    
    List<Integer> result = new ArrayList<>();
    while (i < nums1.length && j < nums.length) {
        if (nums1[i] < nums2[j]) {
            i++;
        }
        else if (nums2[i] < nums1[i]) {
            j++;
        }
        else {
            result.add(nums1[i]);
            //跳过所有重复的元素
            while (i + 1 < nums1.length && nums1[i+1] == nums1[i]) {
                i++;
            }
            i++;
            while (j + 1 < nums2.length && nums2[j+1] == nums2[j]) {
                i++;
            }
            j++;
        }
    }
    return resuilt.toArray();w
}
```



