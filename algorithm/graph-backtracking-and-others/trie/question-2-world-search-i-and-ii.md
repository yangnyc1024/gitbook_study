# Question 2 World Search I& II

#### Method 1 DFS 3 all path

High level

* traverse all paths of the graph
* find a path that matches the target words

Middle Level

* each level:&#x20;
  * check current character if it matches the latter
  * if match, go next character
* level by level



```java

static final int[][] DIRS = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
public static List<String> findWordsBruteForce(char[][] board, String[] words) {
    List<String> res = new ArrayList<>();
    for (String word: words) {
        if (exist(board, word))) {
            res.add(word);
        }
    }
    return res;
}

private static boolean exist(char[][] board, String word) {
    boolean[][] visited = new boolean[rows][cols];
    for (int i = 0 ; i < board.length; i++) {
        for (int j = 0; j < board[0].length; j++) {
            if (helper(board, i, j , word, 0, visited)) {
                 return true;
            }
        }
    }
    return false;
}
private static boolean helper(char[][] board, int x, int y, String word, int index, boolean[][] visited) {
    // basic case
    if (index == word.length()) {
        return true;
    }
    //if (visited[x][y]) {
    //    return false;
    //}
    visited[x][y] = true;
    for (int[] dir: DIRS) {
        int neiX = dir[0] + x;
        int neiY = dir[1] + y;
        if (valid(neiX, neiY, board) && visited[neiX][neiY]) {
            if (helper(board, neiX, neiY, word, index + 1, visited)) {
                return true;
            }
        }
    }
    visited[x][y] = false;
    return false;
}
private boolean isValid(char[][] board, int x, int y) {
    return x >=0 && x< board.length && y >=0 && y < board[0].length;
}
```





#### Method 2 Trie Tree + dfs backtracking

* simplified version(word search I): What if we are only given one target word, and we are to find if the word is in the matrix?
* simultaneously traverse the board, and the target word
* (word search II) simultaneously traverse the board and the trie

```java
class TrieNode {
    // maps a character to its corresponding child
    public Map<Character, TrieNode> children;
    public boolean isWord;
    public boolean add(String word) {
        if (search word) {
            return false;
        }
        TrieNode cur = root;
        for (int i = 0; i < word.length(); i++) {
            TrieNode next = cur.children.get(word.charAt(i));
            if (next == null) {
                next = new TrieNode();
                cur.children.put(word.charAt(i), next);
            }
            cur = next;
        }
        cur.isWord = true;
        return true;
    }
}

public static Set<String> findWords(char[][] board, String[] words) {
    // sanity check
    if (board == null || board.length == 0 || board[0].length == 0; || words == null || words.length == 0) {
        throw new IllegalArgumentException("invalid input");
    }
    Set<String> res = new HashSet<>();
    // step one --> build the Trie form the given list of words
    TrieNode root = buildTrie(words);
    final int rows = baord.length;
    final int cols = board[0].length;
    boolean[][] visited = new boolean[rows][cols];
    StringBuilder sb = new StringBuilder();
    
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            helper(board, i, j, root, sb, res, visited);
        }
    }
    return res;
}

private static TrieNdoe buildTrie(String[] words) {
    TrieNode root = new TrieNode;
    for (int i = 0; i < words.size; i++) {
        root.add(words[i]);
    }
    return root;
}


private static void helper(char[][] board, int x, int y, TrieNode root, StringBuilder sb, 
Set<String> res, boolean[][] visited) {
    // visited represents visited cells on the path
    // from (i, j) to (x, y) (excluding (x, y))
    // base cases
    if (isValid(board, x, y)) {
        return;
    }
    if (visited[x][y]) {
        return;
    }
    char ch = board[x][y];
    if (!root.children.contains(ch)) {
        return;
    }
    
    // recursive rule
    root = root.children.get(ch);
    sb.append(ch);
    if (root.isWord) {
        res.add(sb.toString());
        // do not return here because of root.isWord is not a base case
    }
    visited[x][y] = true;
    for (int[] dir: DIRS) {
        int neiX = dir[0] + x;
        int neiY = dir[1] + y;
        helper(board, neiX, neiY, root, sb, res, visited);
    }
    visited[x][y] = false;
    sb.deleteCharAt(sb.length() - 1);
}

private boolean isValid(char[][] board, int x, int y) {
    return x >= 0 && x< board.length && y >=0 && y < board[0].length;
}
```

