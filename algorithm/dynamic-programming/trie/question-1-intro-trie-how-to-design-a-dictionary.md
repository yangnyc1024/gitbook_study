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



#### Base Operations: 3. delete “apple” from the trie



#### Base Operations: 4. find all the words in a given prefix

