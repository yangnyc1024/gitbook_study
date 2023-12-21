# Question 7 Reverse String II

Middle Level:

* 找一个k size的sliding window
  * 如果left出界，表示结束了
  * 如果right出界，表示全部reverse
* 根据情况选择是否reverse

````java
// Some code

```java
/*
Clarification & Assumption
    - input: String
    - output: string with reverse
    - example: abcdefg ---> bacdfeg
High Level:
    - keep a k length sliding window, reverse its inside and do it iterate

Middle Level:
    - two index left, right
    - left: beginning of the sliding window, which should be reversed
    - right: the end of the sliding window which should be reversed, = min (left + k - 1 , s.length())
    - check until left larger than length, each time left + 2* k;
    - reverse string function
*/

class Solution {
    public String reverseStr(String s, int k) {
        // sanity check
        if (s == null || s.length() == 0) {
            return s;
        }
        if (k < 0) {
            throw new IllegalArgumentException();
        }
        char[] charString = s.toCharArray();
        int left = 0;
        int right = 0;
        while (left < s.length() - 1) {
            right = Math.min(left + k - 1, s.length() - 1);
            reverse(charString, left, right);
            left += 2 * k;
        }
        return new String(charString);
    }
    private void reverse(char[] charString, int i, int j) {
        while (i < j) {
            char temp = charString[i];
            charString[i] = charString[j];
            charString[j] = temp;
            i++;
            j--;
        }
    }
```
````
