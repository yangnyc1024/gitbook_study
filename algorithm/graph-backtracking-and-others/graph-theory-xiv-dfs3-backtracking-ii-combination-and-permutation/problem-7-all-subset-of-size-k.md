# Problem 7 All Subset of Size K



这道是没有重复的版本

#### Method 1: 加或者不加



```java
public class Solution {
    public List<String> subSetsOfSizeK(String set, int k) {
        List<String> result = new ArrayList<>();
        if (set == null) {
            return result;
        }
        char[] arraySet = set.toCharArray();
        StringBuilder currResult = new StringBuilder();
        helper(result, currResult, 0, arraySet, k);
        return result;
    }
    private void helper(List<String> result, StringBuilder currResult, int curIndexPick, char[] arraySet, int k) {
        if (currResult.length() == k) {
            result.add(currResult.toString());
            return;
        }
        if (curIndexPick == arraySet.length) {
            return;
        } 
        // pick
        currResult.append(arraySet[curIndexPick]);
        helper(result, currResult, curIndexPick + 1, arraySet, k);
        currResult.deleteCharAt(currResult.length() - 1);
        // not pick
        helper(result, currResult, curIndexPick + 1, arraySet, k);
    }
}

```





