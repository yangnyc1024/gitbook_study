# Problem 1 Subset I (combination)母题

#### Method 1: 加或者不加（只对combination问题有效） ==》 要么要么

High Level：题目让我们求出all subsets

* step1:什么是一个解？一个subset是一个解
* step2:如何构造一个解？
  * 每一层是什么？考虑一个元素
  * 分支是什么？要么加，要么不加
  * 在哪里收集解？一共有多少层？有多少元素就有多少层
* index：当前层我正要考虑的元素
* index = length -1这个状态，正要考虑最后一个元素
* index = length，这个状态才是考虑完所有元素的状态

<pre class="language-java"><code class="lang-java">public List&#x3C;List&#x3C;Integer>> subsets(int[] nums) {
<strong>    List&#x3C;List&#x3C;Integer>> result = new ArrayList&#x3C;>(0;
</strong><strong>    if (nums == null || nums.length == 0) {
</strong><strong>        return result;
</strong><strong>    }
</strong><strong>    List&#x3C;Integer> curResult = new ArrayList&#x3C;>();
</strong><strong>    backTracking(resul,t nums, curResult, 0);
</strong><strong>    return result;
</strong>}
// index ：当前层我正要考虑的元素
private void backTracking(List&#x3C;List&#x3C;Integer>> result, int[] nums, List&#x3C;Integer> curResult, int index) {
    if (index = nums.length) {
        result.add(new ArrayList&#x3C;>(current));
        return;
    }
    // add
    current.add(nums[index]);
    backTracking(result, nums, current, index + 1);
    current.remove(current.size() - 1);
    // not add
    backTracking(result, nums, current, index + 1);
}
</code></pre>

Question to deep dive: 能不能先写这个不加，这样是不是就可以不用吐了

* 万万不可
* 吃吐必须守恒，就算没有显示的吐，也一定通过某种方式达到吐的效果，直接吃掉吐又没有做任何补充，肯定不对！
* 原因是什么？在一个path上visited过的不能再visited？
