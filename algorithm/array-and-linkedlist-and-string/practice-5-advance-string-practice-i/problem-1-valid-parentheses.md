# Problem 1 Valid Parentheses



1. 需要一个map记录迷一种右括号应该对应的左括号是谁
2. 需要知道离我最近的（最后一个加入）开放着的左括号是哪个-------LIFO逻辑



two pointers:

* i repesent 我需要保留的，j表示我现在在explore的





```java
public boolean isValid(String s) {
    // assume s is valid
    Map<Character, Character> map = new HashMap<>();
    map.put("(", ")");
    map.put("[", "]");
    map.put("{", "}");
    
    char[] array = s.toCharArray();
    int i = 0; // i represents the idx we would like to keep (like the top of the stack)
    // j represents the idx we would like to explore
    for (int j = 0; j < array.length; j++) {
        if ("{[(".indexOf(array[j])) {
            array[i] = array[j];
            i++;
        }
        else if ("}]".indexOf(array[j])) {
            if (i == 0 || array[i - 1] != map.get(array[j])) {
                return false;
            }
            i--;
        }
    }
    return i == 0;
}
```

