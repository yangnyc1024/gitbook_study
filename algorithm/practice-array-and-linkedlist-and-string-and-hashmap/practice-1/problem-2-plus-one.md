# Problem 2 Plus One



```java
public String addBinary(int[] digits) {
    List<Integer> result = new ArrayList<>();
    int i = digits.length - 1;    
    int j = b.length() - 1;
    int carry = 1;    
    while (i >= 0){
        // int sum = carry + int(a[i] + b[i]);
        int sum = carry + digits[i];
        result.add(sum % 10);
        carry = sum / 10; 
        i--;
    }
    if (carry != 0) {
        result.add(carry);
    }
    int[] resultArray = new int[result.size()];
    for (int i = result.size() - 1; i >= 0; i--) {
        resultArray[result.size() - 1 - i] = result.get(i)
    }
    return resultArray;
}
```
