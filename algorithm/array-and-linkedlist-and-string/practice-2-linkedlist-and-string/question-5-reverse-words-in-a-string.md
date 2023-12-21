# Question 5 Reverse Words in a String

* 注意如何找word开头和结尾
  * word 开头的定义：这一个不是space +（ 这是第一个 or 前一个字母是space）
  * word结尾的定义：这一个不是space + （这是最后一个 or后一个是space）
* 注意找可以留下来的
  * word不是space
  * word是第一个space：自己是space + （前一个不是space + 不是第一个）
* 注意trim的结尾

````java
// Some code


```java
/*
clarification & assumption: 
    - string with repeated characters and space
high level:
    - reverse all and reverse each word and trim 
middle level:
    - reverse whole string reverse(word, i, j)
    - reverse each word from the begin char with two pointers
        // find slow and fast pointer until slow reach the length
        // slow pointer: the first char (the previous is ' ' or the first char) and the current is not ' ')   
        // fast pointer: the last char (the current is not ' ', the last one or the next is ' ')        
    - trim the space
        // two pointer fast and slow
        // fast pointer: to explore the space
            - if fast pointer is not " ", keep it， keep it,
            - if fast pointer is " " but it is the first space(first one, or previous is != ' '), keep it,
        // slow pointer: from 0 to current slow index - 1, all char will be remained
        // postprocessing: if char[slow] is " ", slow--;
tc & sc: O(n), O(n)
*/


class Solution {
    public String reverseWords(String s) {
        if (s == null || s.length() == 0) {
            return s;
        }

        // reverse whole string
        char[] originalString = s.toCharArray();
        reverString(originalString, 0, originalString.length - 1);

        // reverse each word
        reverWord(originalString);

        // reverse each word with two pointer and skip the extra space
        String returnValue = trim(originalString);        
        return returnValue;
    }
    private String trim (char[] originalString) {
        int slow = 0;
        int fast = 0;
        while (fast < originalString.length) {
            if (originalString[fast] == ' ' && (fast != 0 && originalString[fast - 1] != ' '))  {
                originalString[slow] = originalString[fast];
                slow++;
            }
            else if (originalString[fast] != ' '){
                originalString[slow] = originalString[fast];
                slow++;
            }
            fast++;
        }
        // corner case
        if (slow > 0 && originalString[slow - 1] == ' ') {
            slow--;
        }
        return new String(originalString, 0, slow);
    }
    private void reverWord(char[] originalString) {
        int left = 0;
        for (int i = 0; i < originalString.length; i++) {
            if (originalString[i] != ' ' && (i == 0 || originalString[i - 1] == ' ')) {
                left = i;
            }
            if (originalString[i] != ' ' && (i == originalString.length - 1 || originalString[i + 1] == ' ')) {
                reverString(originalString, left, i);
            }
        }
    }
    private void reverString(char[] originalString, int left, int right) {
        while (left < right) {
            char temp = originalString[left];
            originalString[left] = originalString[right];
            originalString[right] = temp;
            left++;
            right--;
        }
    }    
}
```
````
