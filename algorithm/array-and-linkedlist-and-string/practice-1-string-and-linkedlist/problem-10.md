# Problem 10



key point：找到mid node

option 1:

* 数一下一共有多少的node
* 再从头出发走n/2个node

option 2:

* 快慢指针，过例子看
  * 初始条件：slow = fast = head
  * 截止条件：fast == null/ fast.next == null

<pre class="language-java"><code class="lang-java"><strong>
</strong><strong>ListNode deleteMiddle(ListNode head) {
</strong><strong>    if (head == null) {
</strong>    return null;
    }
    ListNode dummy = new ListNode();
    dummy.next = head;

    ListNode prev = dummy;
    ListNode slow = head;
<strong>    ListNode fast = head;
</strong>    while (fast != null || fast.next != null) {
        slow = slow.next;
        prev = prev.next;
        fast = fast.next.next;
    }
    prev.next = slow.next;
    return dummy.next;
<strong>}
</strong><strong>
</strong></code></pre>
