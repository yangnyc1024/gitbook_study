# Question4 Reverse Vowels of a String

````java
// Some code

/*
clarification & assumption
    - input: regular string 
    - output: string
    - example: hello 
        - if left is not vowels, left++
        - if right is not vowels, right--;
        - if both are vowels swap
        - until two index same
high level: two index, until swap all
middle level: see example
tc & sc : O(n), O(1)

*/


class Solution {
    public String reverseVowels(String s) {
        // sanity check
        if (s == null || s.length() == 0) {
            return s;
        }
        Set<Character> vowelMap = buildMap();
        char[] charString = s.toCharArray();

        int left = 0;
        int right = s.length() - 1;
        while (left < right) {
            if (!vowelMap.contains(charString[left])) {
                left++;
            }
            else if (!vowelMap.contains(charString[right])) {
                right--;
            }
            else {
                swap(charString, left, right);
                left++;
                right--;
            }
        }
        return new String(charString);
    }
    private void swap(char[] charString, int left, int right) {
        char tmp = charString[left];
        charString[left] = charString[right];
        charString[right] = tmp;
    }
    private Set<Character> buildMap() {
        Set<Character> vowelMap = new HashSet<>();
        vowelMap.add('a');
        vowelMap.add('e');
        vowelMap.add('i');
        vowelMap.add('o');
        vowelMap.add('u');
        vowelMap.add('A');
        vowelMap.add('E');
        vowelMap.add('I');
        vowelMap.add('O');
        vowelMap.add('U');
        return vowelMap;
    } 
}
```
````
