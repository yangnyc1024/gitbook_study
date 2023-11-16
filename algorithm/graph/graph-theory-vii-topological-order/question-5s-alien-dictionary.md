# Question 5s Alien Dictionary

cannot pass all test case in leetcode

```java
/*

Clarification
- input: array of string?
- output:
- example:  like an dictionary

Assumption:
- Graph?
    - vertex: any character
    - edge: sorted lecxicographically could be found in the words(any two adjacent words)

High Level
    - use dfs/bfs to sorted it and find topoloical order

Middle Level - bfs

    - build Graph?
        - check two closed words, find the first not same element, first[i] --> second[i]
        - graph <Char, Set<Char>>
    - build inDegree?
        - inDegree <Char, int>
    - bfs traversal
    - check two things
        - isCycle?
        - topoloical order

Time & Space
    - O (|V| + |E|) = O(|V| + min(|V|^2 + N))
    - O (|V|) = O(1)
*/


class Solution {
    Map<Character, Set<Character>> graph  = new HashMap<>();
    Map<Character, Integer> inDegree = new HashMap<>();
    class ReturnType {
        boolean isCycle;
        String finalString;
        public ReturnType(boolean isCycle, String finalString) {
            this.isCycle = isCycle;
            this.finalString = finalString;
        }
    }
    public String alienOrder(String[] words) {
        // sanity check?

        // build graph
        buildGraph(words);
        // build inDegree map


        // bfs
        ReturnType result = bfs(words);


        // return String/ isCycle
        if (result.isCycle == true) {
            return "";
        }
        return result.finalString;

    }
    private ReturnType bfs(String[] words) {
        boolean isCycle = false;
        StringBuilder dictString = new StringBuilder();
        // initial queue
        Queue<Character> queue = new ArrayDeque<>();
        for (Character cur: inDegree.keySet()) {
            if (inDegree.get(cur) == 0) {
                queue.offer(cur);
                dictString.append(cur);
            }
            // if (dictString.length() == graph.size() && dictString.length() != 1) {
            //     isCycle = true;
            // }
        }
        // expand & generate
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Character cur = queue.poll();
                for (Character next: graph.get(cur)) {
                    inDegree.put(next, inDegree.get(next) - 1);
                    System.out.println(inDegree.get(next));
                    if (inDegree.get(next) == 0) {
                        queue.offer(next);
                        dictString.append(next);
                    }
                }
            }
        }
        // result
        String finalString = dictString.toString();
        if (finalString.length() != graph.size()) {
            isCycle = true;
        }
        return new ReturnType(isCycle, finalString);
    }
    private void buildGraph(String[] words) {
        for (int j = 0; j < words[0].length(); j++) {
            graph.putIfAbsent(words[0].charAt(j), new HashSet<>());
            inDegree.putIfAbsent(words[0].charAt(j), 0);
        }
        for (int i = 1; i < words.length; i++) {
            for (int j = 0; j < words[i].length(); j++) {
                graph.putIfAbsent(words[i].charAt(j), new HashSet<>());
                inDegree.putIfAbsent(words[i].charAt(j), 0);
            }
        }
        for (int i = 1; i < words.length; i++) {
            char[] twoElement = findCompare(words[i -1], words[i]);
            char prev = twoElement[0];
            char next = twoElement[1];
            if (prev != next && !graph.get(prev).contains(next)) { //后面这个condition。。。
                graph.get(prev).add(next);
                inDegree.put(next, inDegree.get(next) + 1);
            }
            System.out.println(graph);
        }

    }
    private char[] findCompare(String previous, String cur) {
        char[] returnElement = new char[2];
        int checkLen = Math.min(previous.length(), cur.length());
        for (int count = 0; count < checkLen; count++) {
            if (previous.charAt(count) != cur.charAt(count)) {
                char preEle = previous.charAt(count);
                char nexEle = cur.charAt(count);
                returnElement[0] = preEle;
                returnElement[1] = nexEle;
                break;
            }
        }
        return returnElement;
    }
}
```
