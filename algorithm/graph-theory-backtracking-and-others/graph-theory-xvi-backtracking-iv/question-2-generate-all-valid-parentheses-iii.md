# Question 2 Generate All Valid Parentheses III

#### Following  up方向

* 1 括号种类对合法性的影响

Key Point 1: 如何处理合法性？指增加括号种类，不考虑优先级，只考虑合不合法

* 本质：增加了加右括号的限制（不管有多少种括号，本质不变）

对于只有小括号的题目

* 加左括号的条件：只要有就能加
* 加右括号的条件：已经加过的左括号的数量》 已经加过的右括号数量

对于既有小括号，又有中括号的题目

* 加左括号的条件：只要有就能加
* 加右括号的条件：不仅加过的我这种左括号得比我这种右括号多，上一个（那么多加过的还open着的左括号呢，我得看看那个最后一次添加的）未匹配中最后一次添加的左括号必须与我同种（match）
* < ) not OK, (<)> not Ok also !!1



对于这道题，N种括号的题目

* 加左括号的条件：只要有就能加
* 加右括号的条件：不仅加过的我这种左括号得比我这种右括号多，上一个（那么多加过的还open着的左括号呢，我得看看那个最后一次添加的）未匹配中最后一次添加的左括号必须与我同种（match）



2 优先级

Key Point 2: 如何处理优先级

本质：增加了加左括号的限制（不管有多少种优先级，本质不变）

* （<  not OK 优先级错误 &&()<> OK

题目引入了优先级：左括号变得不是那么随意 不能有就加了

加左括号的条件：上一个（那么多加过的还openopen着的左括号呢，我得看看那个最后一次添加的）未匹配中最后一次添加的左括号， 必须，大于等于，我现在要加的左括号的优先级





概念：上一个加的左括号 ！=上一个未匹配的左括号

Modeling:如何Model括号的优先级: Map +数字



```java
public class Solution {
    private static final char[] allP = {
        '(', ')',   '<', '>',   '{', '}',
    }
    public List<String> ValidParenthese(int l, int m, int n) {
        List<String> result = new ArrayList<>();
        Map<Character, Integer> priority = new HashMap<>();
        priorty.put("(", 0);
        priorty.put("<", 1);
        priorty.put("{", 2);
        StringBuilder sb = new StringBuilder();
        Deque<Character> stack = new ArrayQueue<>();
        int[] remain = {l, l, m, m, n ,n};
        int total = 2 * l + 2 * m + 2 * n;
        DFS(remain, result, total, sb, stack, priority);
        return result;
    }

}
```



