# Question 1 Intro Trie: How to design a dictionary

#### 1. What is the requirement of this dictionary?

* search(word)
* delete
* add

#### 2. Options for data structures

n- # of words

m - the average length of the string/word

* HashMap.contain(target)
  * hashCode: O(m)
  * string compare: O(m)
* Binary Search Tree (Treeset)
* ArrayList(sorted, unsorted)
* Trie

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-06 at 3.57.51 PM.png" alt=""><figcaption></figcaption></figure>

#### What is Trie

* Retrieve, prefixTrie,
* a data structure, more precisely, a search tree

Tries are different from binary search tree

* a key is associated with a "path from the root" to a node, instead of associated with a node(说白了就是你的字母是在边上，所以单词在path上)
* the edges from a node represent distinct character

The path from the root to each node is <mark style="color:purple;">a prefix</mark> of a word in the dictionary,因此也叫前缀树

#### Trie class

```java
class TrieNode {
    // Map a character to its corresponding child
    // 以前的tree child对应的是一个个点，这次是以character作为1，2，3
    Map<Character, TrieNode> children;
    boolean isWord; //这个点是不是作为结束
    int value; // optional. a set doesn't nee this field
}


class TrieNode {
    // an array of size 26, each index --> character
    TrieNode[] children;
    boolean isWord; //这个点是不是作为结束
    int value; // optional. a set doesn't nee this field
}
```

#### TC& SC

Time: worst case guarantee O(m)

Space: worst case O(mn), but usually much better than this. \
\- if the trie is dense, since reusing the common prefix as many as possible, less space is required

#### Drawbacks

Trie's advanced drawbacks(在硬盘里常有问题)

time\
\- if stored on disk, more random disk accesses(very expensive)

space\
\- every trieNode has extra space consumption--> extra space usage\
\- memory allocation fragmentation, especially when the trie is sparse

#### Use Case

* string or sequence type elements
* fast worst-case search/add/delete
* grouping common prefixes, both for time/space efficiency
* especially when the trie to prefix/matching



#### Base Operations: 1. search "cat" in the trie

```java
// finding the path from root which is equal to 'cat'
// for reach of the characters in "cat", see if there is an edge associated with it for the next level
public boolean search(String word) {
    TrieNode cur = root;
    for (int i = 0; i < word.length(); i++) {
        TrieNode next = cur.children.get(word.charAt(i));
        if (next == null) return false;
        cur = next;
    }
    return cur.isWord;
}

// Time: O(word.length)
```

#### Base Operations: 2. add "carp" into the trie

```java
// finding the path from root which is equal to "carp"
// for each of the character in "carp", see if there is an edge associated with it for the next level
// 1. if there is an edge, go to the corresponding child node
// 2. if there is not, create the child node

public boolean insert(String word) {
    if (search(word)) {
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
        // cur.count++;
    }
    cur.isWord = true;
    return true;
}
// TC: O(word.length)
```



#### Base Operations: 3. delete “apple” from the trie

Solution 1:&#x20;

* Store the path from root to the to-delete node in a stack
* Mark the last node as not word
* When popping a node form the stack, erase the node if it is not a word and has no children

Solution 2:

* 所以你再遍历你这个word，然后呢，每次看这接下来有几个单词，如果只剩一个了，剩下的全删了

```java

class TrieNode{
    int count; // how many word are on this subtree(inclusive)
    Map<Character, TrieNode> children;
    boolean isWord; // indicate if the node is the end of the word
}


public boolean delete(String word) {
    if (!search(word)) {
        return false;
    }
    root.count--; //你每一次都需要delete
    TrieNode cur = root;
    for (int i = 0; i < word.length(); i++) {
        TrieNode next = cur.children.get(word.charAt(i));
        next.count--;
        if (next.count == 0) {
            cur.children.remove(word.charAt(i));
            return true;
        }
        cur = next;
    }
    cur.isWord = false; // e.g. app
    return true;
}

// Time O(word.length)
```

#### Base Operations: 4. find all the words in a given prefix

for example find all with prefix "ca"

* step 1: find the node x associated with prefix "ca"
* step 2: do DFS on the subtree rooted at x to find all words



Option 1:偷懒就是在这个点上已经存储了，否则你要存path

```java

// option 1
class TrieNode {
    // Maps a character to its corresponding child
    Map<Character, TrieNode> children;
    boolean isWord;
    int value; // optional, a set doesn't need this field
    string word;
}

public void findAllWordsUnderNode(TrieNode current, List<String> result) {
    if (current.isWord) { // this is when we find a word.
        result.add(current.word);
        // shall we return here? No, children可能还有word
    }
    // find all branches
    for (Entry<Character, TrieNode> child: current.children.EntrySet()) {
        findAllWordsUnderNode(child.getValue(), result);
    }
}


```

Option 2:你就是要记录这个stringBuilder

```java
public List<String> findAllWordsWithPrefix(TrieNode root, String prefix) {
    TrieNode matchNode = searchNode(root, prefix); // 你要先找到前缀
    if (matchNode == null) {
        return result;
    }
    List<String> result = new ArrayList<>();
    findAllWordsUnderNode(matchNode, new StringBuilder(prefix), result);
    return result;
}

public void findAllWordsUnderNode(TrieNode current, StringBuilder curPath, List<String> result) {
    if (current.isWord) { // this is  when we find a word
        result.add(curPath.toString());// we should not return here, children might have word
    }
    // all branches
    for (Entry<Character, TrieNode> child: current.children.EntrySet()) {
        curPath.append(child.getKey());
        findAllWordsUnderNode(child.getValue(), curPath, result);
        curPath.deleteCharAt(curPath.length() - 1);
    }
}
```

TC \* SC: O(search) + O(# of result words) = O(height) + O(# of result words)

It can be extended to support more operations, what other possible queries can it support?

* Wildcard expression match queries
* regular expression match queries
* words winthin certain edit distance

e.g. Wildcard

* "?" means single character. //.
* "\*" means >= 0 arbitrary characters. //>=0
