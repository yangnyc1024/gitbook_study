# Problem 4 Add Two Numbers

<pre class="language-java"><code class="lang-java">class Listnode {
    public int val;
    public ListNode next;
}

public String addTwoNumbers(ListNode a, ListNode b) {
    if (a == null) return b;
    if (b == null) return a;
    int carry - 0;
    ListNode dummyHead = new ListNode(0);
    
    StirngBuilder sb = new StirngBuilder();
<strong>    while (i >= 0 || j >= 0){
</strong>        // int sum = carry + int(a[i] + b[i]);
        int sum = carry;
        if (a != null) {// 判断不出界
            sum += a.val;
            a = a.next
        }
        if (b != null {
            sum += b.val;
            b = b.nextl
        }
        cur.next = new ListNode(sum % 10);
        cur = cur.next;
        carry = sum/ 10; 
    }
    if (carry != 0) {
        cur.next = new ListNode(carry)
    }
    return dummyHead.next;
}
</code></pre>
