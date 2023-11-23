# Question 0 Get Roman Number

```java
public String getRomanNumber(int num) {
    String[] roman = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < number.length && num > 0 ; i++) {
        while (num >= numbers[i]) {
            num -= number[i];
            sb.append(roman[i]);
        }
    }
    return sb.toString();
}
```
