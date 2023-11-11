# Question 6 Reverse String



````java
// Some code

```java
/*
classification& assumption:
    - char[]
high level: reverse pair from head and tail until we reverse all

middle level:
 - have two index
 - each iteratation, we add left and minus right until index becomes same
    - swap
    - left++ ,right--
TC & SC: O(n), O(1)
*/

class Solution {
    public void reverseString(char[] s) {
        // sanity check
        if (s == null || s.length == 0) {
            return;
        }
        int left = 0;
        int right = s.length - 1;
        while (left < right) {   
            swap(s, left, right);
            left++;
            right--;
        }
    }
    private void swap(char[] s, int left, int right) {
        char temp = s[left];
        s[left] = s[right];
        s[right] = temp;
    }
}
```
````
