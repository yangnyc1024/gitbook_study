# Problem 8 All Subset II of Size K

Method 1: 加或者不加

```java
public class Solution {
  public List<String> subSetsIIOfSizeK(String set, int k) {
    // sanity check
    List<String> result = new ArrayList<String>();
    if (set == null) {
      return result;
    }
    char[] arraySet= set.toCharArray();
    Arrays.sort(arraySet);
    StringBuilder curResult = new StringBuilder();
    helper(result, curResult, 0, k, arraySet);
    return result;
  }
  private void helper(List<String> result, StringBuilder curResult, int curIndex, int setSize, char[] arraySet) {
    if (curResult.length() == setSize) {
      result.add(new String(curResult));
      return;
    }
    if (curIndex == arraySet.length) {
      return;
    }
    // // add
    // curResult.append(arraySet[curIndex]);
    // helper(result, curResult, curIndex + 1, setSize, arraySet);
    // curResult.deleteCharAt(curResult.length() - 1);
    // // not add
    // while (curIndex + 1 < arraySet.length && arraySet[curIndex] == arraySet[curIndex + 1]) {
    //   curIndex++;
    // }
    // helper(result, curResult, curIndex + 1, setSize, arraySet);
    int originalIndex = curIndex;
    while (curIndex < arraySet.length - 1 && arraySet[curIndex] == arraySet[curIndex + 1]) {
      curIndex++;
    }
    helper(result, curResult, curIndex + 1, setSize, arraySet);

    curIndex = originalIndex;
    curResult.append(arraySet[curIndex]);
    helper(result, curResult, curIndex + 1, setSize, arraySet);
    curResult.deleteCharAt(curResult.length() - 1);
  }
}
```

解法可参照problem 1

Method 2: 每一次都加？

```java
public class Solution {
  public List<String> subSetsIIOfSizeK(String set, int k) {
    // Write your solution here
    List<String> result = new ArrayList<>();
    if (set == null) {
      return result;
    }
    char[] charSet = set.toCharArray();
    StringBuilder curString = new StringBuilder();
    Arrays.sort(charSet);
    dfs(charSet, curString, k, 0, result);
    return result;
  }
  private void dfs(char[] charSet, StringBuilder curString, int k, int index, List<String> result) {
    if (curString.length() == k) {
      result.add(new String(curString));
    }
    if (curString.length() > k) {
      return;
    }
    for (int i = index; i < charSet.length; i++) {
      if (i == index || charSet[i] != charSet[i - 1]) {
        curString.append(charSet[i]);
        dfs(charSet, curString, k, i + 1, result);
        curString.deleteCharAt(curString.length() - 1);
      }
    }
  }
}
```
