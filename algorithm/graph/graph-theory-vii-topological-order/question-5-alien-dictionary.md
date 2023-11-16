# Question 5 Alien Dictionary





有没有可能有特殊情况：

* case1:前面不是空，后面是空
  * \["ab" ,“”] invalid edge
* case2: 公共部分完全一样，前面这个单词比后面章
  * \["ab", "a"] invalid case 无法知道a和b的关系, return&#x20;





```java

private static final List<Character> EMPTY_LISt = new ARrayList<>();
private static final int ALLSET = 26;
public String alienOrder(String[] words) {
    Map<Character, Integer> inDegrees = new HashMap<>();
    Map<Character, List<CHaracter>> graph = new HashMap<>();
    //不是全部的node都一定存在于indegree Map里面
    Set<Character> allNodesFromDict = new HashSet<>();
    
    
    // step 1: build graph
    for (int i = 1; i < words.length; i++) {
        String w1 = words[i - 1];
        String w2 = words[i];
        for (int j = 0; j < Math.min(w1.length(), w2.length()); j++) {
            char c1 = w1.charAt(j);
            char c2 = w2.charAt(j);
            if (c1 != c2) {
                if (!graph.containsKey(c1)) {
                    graph.put(c1, EMPTY_LIST);
                }
                graph.get(c1).add(c2);
                inDegree.put(c2, inDegree.getOrDefault(c2, 0) + 1);
                allNodesFromDict.add(c1);
                allNodesFromDict.add(c2);
                break;
            }
        }
        //第一个字母比较长，第二个字母比较短，公共
    }
    
    
    // Step2 : BFS Topological Sort
    // Step 2.1
    Deque<Character> queue = new ArrayDeque<>();
    for (Character ch: allNodesFromDict) {
        // if(inDegrees.getOrDefault(ch, 0) == 0) {
        if (!inDegrees.containsKey(ch)){
            queue.offer(ch);
        }
        
        /*
        Question 1: 能不能写成inDegrees.get(ch) ? NPE
        */
    }
    
    
    // Step 2.2 BFS
    
    // Step 2.3 check cycle
    if (sb.length() != allNodesFromDict.size ()) {
        return "";
    }
    
    // Step 3:还原最终结果，无关字母来自于哪里（需要问面试官）：如果来自于wordList，我们需要知道有哪些字母在word List里但不在stringBuilder里面
    Set<Character> allNodes = new HashSet<>();
}
```



TC& SC

TC:

* BuildGraph + BFS topological sort + Reconstruct the order
  * dict.legnth+ longestWord \* longestWord
  * 26\*26
  * dict.length \* longestWord + sb.length() + dict.length()
* O(26^2 + 3\*dict.length\* longestWord +sb.length())

SC:

* Graph: Map\<Character, List\<Chacter>>
* Indegree: Map\<Character, Integer>
* Set\<Character> notSame
* Set\<Character> allNodes
* StringBuilder for topo, queue in BFS





