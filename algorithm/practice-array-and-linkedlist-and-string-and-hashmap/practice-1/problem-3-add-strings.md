# Problem 3 Add Strings

```java
public String addBinary(String a, String b) {
    int i = a.length() - 1;
    int j = b.length() - 1;
    int carry - 0;
    StirngBuilder sb = new StirngBuilder();
    while (i >= 0 || j >= 0){
        // int sum = carry + int(a[i] + b[i]);
        int sum = carry;
        if (i >= 0) {// 判断不出界
            sum += a.charAt(i) - '0';
        }
        if (j >= 0) {
            sum += b.charAt(j) - '0';
        }
        carry = sum / 10; 
        sb.append(sum % 10);
        i--;
        j--;
    }
    if (carry != 0) {
        sb.append(carry);
    }
    return sb.reverse().toString();
}
```
