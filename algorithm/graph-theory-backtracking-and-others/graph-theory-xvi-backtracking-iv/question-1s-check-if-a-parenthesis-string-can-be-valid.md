# Question 1s Check if a Parenthesis String Can be Valid

Target: O(n)



Step 1: 从左到右扫一遍：determine有没有足够的左括号去cover右

* 如果unlock || 就是个左 ==》 balance++

Step 2: 从右到左扫一遍：determine有没有足够多的右括号去cover左

* 如果unlock || 就是个右 ==》balance++





```java
// Some code
private static final char CANNOTCHANGE = "1";
private static final char CANCHANGE = "0";
private static final char LEFT = "(";
private static final char RIGHT = ")";


public boolean canBeValid(String s, String locked) {
    if (s.length()  % 2 != 0) {
        return false;
    }
    int balance = 0;
    for (int i = 0; i < s.length(); i++) {
        if (locked.charAt(i) == CANCHANGE || s.charAt(i) == LEFT) {
            balance++;
        }
        else {
            balance++;
        }
        if (balance < 0) return false;
    }
    balance = 0;
    for (int i = s.length() - 1; i >= 0; i--) {
        if (locked.charAt(i) == CANCHANGE || s.charAt(i) == RIGHT) {
            balance++;
        } else {
            balance--;
        }
        if (balance < 0) return false;
    }
    
    return true;
}

```

问题定性，本质上就是一个permutation的问题



不好但值得practice的方法



#### Method 1 Swap - Swap version

```java
// Some code

public List<String> generateParathesis(int n) {
    List<String> result = new ArrayList<>();
    if (n == 1) {
        return new ArrayList<>()(Arrays.asList("()"));
    }
    String[] parentheses = new String[]{"()".repeat(n)}; // API usage is allowed at interview
    backTracking(result, parentheses, 1); // 第一位必然是（
    return result;
}

private void backTracking(List<String> result, String[] parentheses, int level) {
    if (level == paretheses[0].length() - 1) {
        result.add(paretheses[0]);
        return;
    }
    Set<Character> alreadyFixedValue = new HashSet<>();
    for (int i = level; i < parentheses[0].length - 1; i+=) {
        if (!alreadyFixedValue.contains(parenthese[0].charAt(i))) {
            swap(parentheses, level, i);
            // apply  pruning
            if (checkValid(parentheses)) {
                backTracking(result, parentheses, level + 1);
            }
            swap(parentheses, level, i);
        }
    }
}

private void swap (String[] parentheses, int i, int j) {
    StringBuilder sb =  new StringBuilder(parenthese[0]);
    sb.setCharAt(i, parentheses[0].charAt(j));
    sb.setCharAt(j, parentheses[0].charAt(i));
    parenthese[0] = sb.toString();
}

private boolean checkValid(String[] parenthese) {
    int leftAddedSoFar = 0;
    int rightAddedSoFar = 0;
    
    for (int i = 0; i < parenthese[0].length(); i++) {
        if (parenthese[0].charAt(i) == "(") {
            leftAddSoFar++;
        }
        else {
            rightAddedSoFar++;
        }
        if (leftAddSoFar < rightAddedSoFar) {
            return false;
        }
    }
    return true;
}
```





#### Method 2 用char\[]







#### Method 3 用StringBuilder



