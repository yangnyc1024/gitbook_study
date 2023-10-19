# Question 2 Word Ladder I



## Method 1 DFS backtracking



## Method 2 BFS

### High level

* this is a graph problem,
  * vertex：每个单词就是一个点
  * edge：在wordList里面和自己只相差一个字典的单词都是neighbor
* therefore, this problem is asking about the shortest path problem
  * from start node to target node
  * unit weight shortest path problem
  * method BFS
* High level of BFS
  * Expansion: 每一次我从Queue里poll处当前层需要expand(visit)的node
  * Generation：得有办法找到wordList里所有和当前层expand的word相差一个字的

### Details

* generation这一步怎么做？

#### Method 1: Brute Force

```java
// Some code
public List<String> getAllTheNeighborWords(String cur, Set<String> wordList) {
    List<String> result = new ArrayList<>();
    for (String word: wordList) {
        if (isNei(word, cur)) {
            result.add(word);
        }
    }
    return result;
}

private boolean isNei(String cur, String word) {
    if (word.length() != cur.length) {
        return false;
    }
    int count = 0;
    for (int i = 0; i < cur.length(); i++)  {
        if (cur.charAt(i) != word.charAt(i)) {
            count++;
            if(count > 1) {
                return false;
            }
        }
    }
    return true;
}

```

#### Method 2 自己探索隐藏的图

* 直接从单词本身出发==》 从Node本身出发去找neighbor
* 遍历这个单词，尝试替换每个单词中的每个字母，看看这个单词在不在wordList里面

```java
// Some code
public List<String> getAllTheNeighborWords(String cur; List<String> wordList) {
    List<String> result = new ArrayList<>();
    char[] array = cur.toCharArray();
    
    for (int i = 0; i < array.length; i++) {
        char temp = array[i];
        for (char j = 'a' ; j <= 'z'; j++) {
            if (temp != j) {
                array[i] = j;
                String newWord = new String(array);
                if (wordList.contains(newWorld)) {
                    result.add(newWorld);
                }
                array[i] = temp; //一定要换回
             }
        }
        // array[i] = temp; // better
    }
    return result;
}
```

```java
// Some code
public int ladderLength(String beginWord, String endWord, List<String> wordList) {
    Set<String> wordSet= new HashSet<>();
    for (String word: wordList) {
        wordSet.add(s);
    }
    Deque<String> queue = new ArrayDeque<>(0l
    Set<String> visited = new HashSet<>();
    queue.offer(beginWord);
    visited.add(beginWord);
    int level = 1;
    
    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            String cur = queue.poll();
            List<String> allNeighbors = getAllTheNeightborWords(cur, wordSet);
            if (!allNeighbors.isEmpty()) {
                for (String nei: allNeighbors) {
                    if (nei.equals(endWord)) {
                        return level + 1;
                    }
                    if (!visited.contains(nei)) {
                        queue.offer(nei);
                        visited.add(nei);
                    }
                }
            }
        }
        level++;
    }
    return 0;
}
```



#### Clarification && Assumption:

* StartWord 和 EndWord一样怎么办
* EndWord or StartWord 不在wordList里怎么办
* 到不了return什么？

Modeling Graph

&#x20;
