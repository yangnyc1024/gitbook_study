# Problem 2 Grid Illumination

```java
private static final int[][] DIRS = {{0,0}, {0,1},{1,0}, {-1, 0}, {0, -1}, {1, 1}, {-1, -1},{1, -1}, {-1, 1}};


// 1 stands for 亮
// 2 stands for 不亮

private int[] illumination(int n, int[][] lamps, int[][] queries) {
    int[] result = new int[queries.length];
    Map<Integer, Integer> rows = new HashMap<>();
    Map<Integer, Integer> cols = new HashMap<>();
    Map<Integer, Integer> leftToRightDiags = new HashMap<>();
    Map<Integer, Integer> rightToLeftDiags = new HashMap<>();
    
    // store the 1D version of the index that cords are on
    Set<Integer> lampsOnOrNot = new HashSet<>();
    // step 1:点亮每个灯
    for (int[] lamp : lamps) {
        int row = lamp[0];
        int col = lamp[1];
        
        int id = row*n. + col;
        if (!lampsOnOrNot.contains(id)) {
            row.put(rows, rows.getOrDefault(row, 0) + 1));
            cols.put(rows, cols.getOrDefault(col, 0) + 1));
            leftToRightDiags.put(col - row, leftToRightDiags.getOrDefault(col - row, 0) + 1);
            rightToLeftDiags.put(col + row, rightToLeftDiags.getOrDefault(col + row, 0) + 1);           
        }
    }
    // step 2: 每个query查询加熄灯
    for (int i = 0; i < queries.length; i++) {
        int x = queries[i][0];
        int y = queries[i][1];
        
        if (checkIlluminate(x, y, rows, cols, leftToRightDiags, rightToLeftDiags)) {
            result[i] = ILLU;
        }else {
            result[i] = NOTILLU;
        }
        if (!lampsOnOrNot.isEmpty()) {
            turnOffNeighbors(n, x, y, lampsOnOrNot, rows, cols, leftToRightDiags, rightToLeftDiags);
        }
    }
    return result;
}
// check 灯亮不亮，只要有人能让你亮就ok
private boolean checkIlluminate(int x, int y, Map<Integer, Integer> rows, Map<Integer, Integer> cols, Map<Integer, Integer> leftToRightDiags, Map<Integer, Integer> rightToLeftDiags) {
    return (rows.containsKey(x) && rows.get(x) > 0) ||
            (cols.containsKey(x) && cols.get(y) > 0) ||
            (leftToRightDiags.containsKey(y - x) && leftToRightDiags(y - x) > 0) ||
            (rightToLeftDiags.containsKey(y - x) && rightToLeftDiags(y - x) > 0) 

}



```
