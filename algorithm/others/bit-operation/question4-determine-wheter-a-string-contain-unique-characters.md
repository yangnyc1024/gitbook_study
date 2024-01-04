# Question4 determine wheter a string contain unique characters

Solution 1: hashset

* linear scan ，把坚果的字母都放在hashset里面

```java
// Some code
boolean isUnique(String a) {
    HashSet<Character> set  = new HashSet<>();
    for (int i = 0; i < a.length(); i++) {
        char c = a.charAt(i);
        if (set.contains(c)) {
            return false;
        }
        set.add(c);
    }
    return true;
}
```

Solution2:

* 如果只有有限个，比如说只有lowercase letter “a” --"z"
*
