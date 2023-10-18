# Question 2 Word Ladder kBFS version



* 如果你这一层的点题目没有要求谁先谁后的expand，不一定要用Queue这个媒介，可以直接用个List，Set
* BiD-BFS我们在A测需要知道A侧走到的点在不在B侧的范围内，B侧走到的点在不在A侧的访问内
  * look up operation : Set >>> Queue

```java
public int ladderLength(String beginWord, String endWord, List<String> wordList) {
    Set<String> wordSet = new HashSet<wordList>;
    // assume startWord, endWord all Valid and endWord inside the wordList
    
    wordSet.remove(endWord);
    wordSet.remove(beginWord);
    
    Set<String> forwardQueue = new HashSet<>();
    Set<String> backwardQueue = new HashSet<>();
    forwardQueue.add(beginWord);
    backwardQueue.add(endWord);
    
    int level = 1;
    while(!forwardQueue.isEmpty() && !backwardQueue.isEmpty()) {
        // 特别标准的点图里面，你走一步，我走一步，双侧都是等分支数，等量节点
        // 永远从少的那边走就好了
        if (forwardQueue.size() > backwardQueue.size()) {
            Set temp = forwardQueue;
            forwardQueue = backwardQueue;
            backwardQueue = temp;
        }
        level++;
        
        Set<String> forwardMutation = new HashSet<>();
        for (String word: forwardQueue) {
            // generate word 的neighbor，check这个neighbo是不是合法且对方有没有访问过
            char[] wordChar = word.toCharArray();
            for (int i = 0; i < wordChar.length; i++)  {
                char original = wordChar[i];
                for (char c = 'a'; c <= 'z'; c++) {
                    if (c == original) continue;
                    wordChar[i] = c;
                    String mutation = new String(wordChar);
                    if (backwardQueue.contains(mutation)) {
                        return level;
                    }
                    if (wordSet.contains(mutation)) {
                        forwardMutation.add(mutation);
                        wordSet.remove(mutation);
                    }
                }
                wordChar[i] = original;
            }
        }
        forwardQueue  = forwardMutation;
    }
    return 0;
}
```
