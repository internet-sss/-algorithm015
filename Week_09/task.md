
1.[387. 字符串中的第一个唯一字符](https://leetcode-cn.com/problems/first-unique-character-in-a-string/)
```java
public int firstUniqChar(String s) {
    if (s.length() == 0) return -1;
    HashMap<Character, Integer> map = new HashMap<>();
    for (char c: s.toCharArray()) map.put(c, map.getOrDefault(c, 0) + 1);
    for (int i = 0; i < s.length(); i ++)
        if (map.get(s.charAt(i)) == 1) return i;

    return -1;
}

```

2.[541. 反转字符串 II](https://leetcode-cn.com/problems/reverse-string-ii/)
```java
// 1. 递归
public String reverseStr(String s, int k) {
    if (s.length() < 2) return s;
    StringBuilder sb = new StringBuilder();
    recursion(s, sb, k);
    return sb.toString();
}

private void recursion(String s, StringBuilder sb, int k) {
    int sbLen = sb.length();
    int sub = s.length() - sbLen;
    if (sub >= 2 * k) {
        for (int i = skLen + k - 1; i >= skLen; i --) sb.append(s.charAt(i));
        for (int i = sb.length(); i < sb.length() + k; i ++) sb.append(s.charAt(i));
        recursion(s, sb, k);
    } else if (sub >= k) {
        for (int i = sbLen + k - 1; i >= sbLen; i --) sb.append(s.charAt(i));
        for (int i = sb.length(); i < s.length(); i ++) sb.append(s.charAt(i));
    } else {
        for (int i = s.length() - 1; i >= sbLen; i --) sb.append(s.charAt(i));
    }
}

```

3.[151. 翻转字符串里的单词](https://leetcode-cn.com/problems/reverse-words-in-a-string/)
```java


```

4.[557. 反转字符串中的单词 III](https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/)
```java


```

5.[917. 仅仅反转字母](https://leetcode-cn.com/problems/reverse-only-letters/)
```java


```

6.[205. 同构字符串](https://leetcode-cn.com/problems/isomorphic-strings/)
```java


```

7.[680. 验证回文字符串 Ⅱ](https://leetcode-cn.com/problems/valid-palindrome-ii/)
```java


```

8.[63. 不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/)
```java


```

9.[300. 最长上升子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)
```java


```

10.[91. 解码方法](https://leetcode-cn.com/problems/decode-ways/)
```java


```

11.[8. 字符串转换整数 (atoi)](https://leetcode-cn.com/problems/string-to-integer-atoi/)
```java


```

12.[438. 找到字符串中所有字母异位词](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/)
```java


```

13.[5. 最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)
```java


```

14.[32. 最长有效括号](https://leetcode-cn.com/problems/longest-valid-parentheses/)
```java


```

15.[818. 赛车](https://leetcode-cn.com/problems/race-car/)
```java


```

16.[44. 通配符匹配](https://leetcode-cn.com/problems/wildcard-matching/)
```java


```

17.[115. 不同的子序列](https://leetcode-cn.com/problems/distinct-subsequences/)
```java


```

.[]()
```java


```

.[]()
```java


```