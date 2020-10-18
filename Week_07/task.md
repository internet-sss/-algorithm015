1.[70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)
```java
// 1. 斐波那契数列
public int climbStairs(int n) {
    if (n < 3) return n;

    int one = 1;
    int two = 2;
    for (int i = 3; i <= n; i ++) {
        two += one;
        one = two - one;
    }

    return two;
}

// 2. 额外一维空间，动态规划
public int climbStairs(int n) {
    if (n < 3) return n;

    int[] dp = new int[n + 1];
    dp[1] = 1;
    dp[2] = 2;
    for (int i = 3; i <= n; i ++)
        dp[i] = dp[i - 1] + dp[i - 2];
    
    return dp[n];
}

// 3. 递归，记忆化搜索
public int climbStairs(int n) {

    int[] memory = new int[n + 1];

    return recursion(int n, memory);
}

private int recursion(int n, int[] memory) {
    if (n < 3) return n;

    if (memory[n] > 0) return memory[n];

    int res = recursion(n - 1, memory) + recursion(n - 2, memory);
    memory[n] = res;

    return res;
}

```

.[208. 实现 Trie (前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/#/description)
```java
class Trie {
    Trie[] next = new Trie[26];
    boolean isEnd = false;

    public Trie() {
    }

    public void insert(String word) {
        Trie curr = this;
        for (char c : word.toCharArray()) {
            if (curr.next[c - 'a'] == null) {
                curr.next[c - 'a'] = new Trie();
            }
            curr = curr.next[c - 'a'];
        }
        curr.isEnd = true;
    }

    public boolean search(String word) {
        Trie curr = this;
        for (char c : word.toCharArray()) {
            if (curr.next[c - 'a'] == null) return false;
            curr = curr.next[c - 'a'];
        }
        return curr.isEnd;
    }

    public boolean startsWith(String prefix) {
        Trie curr = this;
        for (char c : prefix.toCharArray()) {
            if (curr.next[c - 'a'] == null) return false;
            curr = curr.next[c - 'a'];
        }
        return true;
    }
}




```

3.[547. 朋友圈](https://leetcode-cn.com/problems/friend-circles/)
```java
class Solution {
    public int findCircleNum(int[][] M) {

        UnionFind friends = new UnionFind(M.length);
        for (int i = 0; i < M.length; i ++) {
            for (int j = 0; j < M.length; j ++) {
                if (M[i][j] == 1 && i != j) friends.union(i, j);
            }
        }
        
        return friends.count();
    }


    class UnionFind {
        private int count = 0;
        private int[] parent;

        public UnionFind(int n) {
            count = n;
            parent = new int[n];
            for (int i = 0; i < n; i ++)
                parent[i] = i;
        }

        public int find(int p) {
            while (p != parent[p]) {
                parent[p] = parent[parent[p]];
                p = parent[p];
            }
            return p;
        }

        public void union(int p, int q) {
            int rootP = find(p);
            int rootQ = find(q);
            if (rootP == rootQ) return;
            parent[rootP] = rootQ;
            count --;
        }

        public int count() {
            return count;
        }
    }
}

```

.[]()
```java


```

.[]()
```java


```

.[]()
```java


```

.[]()
```java


```

.[]()
```java


```

.[]()
```java


```

.[]()
```java


```

.[]()
```java


```

.[]()
```java


```

.[]()
```java


```

.[]()
```java


```