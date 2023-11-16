# Question 3 Similar String Groups

model the question看到这句话&#x20;

* each group is such that a word is in the group iff it is similar to at least one other word in the group

group:联通分量

#### Method 1: DFS

* 需要markVisited + 图不一点联通（必须从每个点出发）
* 点：每个word
* 边：similar word





#### Method 2 Union Find

* 图的问题
  * 每个词是点
  * 边是similar
  * 这道题本质上是问的是你够早的图上的什么问题
    * 有多少个联通分量uf.count问题

Step1: Union find开多长

* strs.length

Step 2: Union 的是什么样的点？

* 两个similar的词

Step 3:结果

* count:剩余多少帮派

notice：

* 只要有时间, union by wieght + path compression
* 没时间就写union by weight 但是加个size数组和if block就完事

<pre class="language-java"><code class="lang-java">public int numberSimilarGroups(String[] strs) {
  int result = 0;
  int count = str.length;
  int[] laoda = new int[count];
  
  for (int i = 0; i &#x3C; count; i++){
    laoda[i] = i;
  }
  for (int i = 0; i &#x3C; strs.length; i++) {
    for (int j = 0; j &#x3C; i; j++) {
      if (isSimilar(strs[i], str[j])) {
        int alaoda = find(laoda, i);
        int blaoda = find(laoda, j);
        if (alaoda != blaoda) {
          count--;
          laoda[alaoda] = blaoda;
        }
      }
    }
  }
  return count;
}
<strong>private int find(int[] laoda, int a) {
</strong>  return laoda[a] = laoda[a] == a? a: find(laoda, laoda[a]);
}

private boolean isSimilar(String a, String b) {
  int diff = 0;
  int i = 0;
  while (i &#x3C; a.length()) {
    if (a.charAt(i) != b.charAt(i)) {
      diff++;
    }
    if (diff > 2) break;
    i++;
  }
  //要么一样，要么至多两个不一样
  return diff == 0 || diff == 2;
}
</code></pre>

