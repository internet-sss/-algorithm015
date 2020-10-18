1.[62. 不同路径](https://leetcode-cn.com/problems/unique-paths/)
```java
// 1. 额外二维空间动态规划
public int uniquePaths(int m, int n) {
    if (n == 1) {
        return 0;
    }

    int[][] dp = new int[m][n];
    for (int i = 0; i < m; i ++) dp[i][0] = 1;
    for (int i = 0; i < n; i ++) dp[0][i] = 1;

    for (int i = 1; i < m; i ++) {
        for (int j = 1; j < n; j ++) {
            dp[i][j] = dp[i][j - 1] + dp[i - 1][j];
        }
    }

    return dp[m - 1][n - 1];
}

// 2. 额外一维空间动态规划
public int uniquePaths(int m, int n) {
    if (n == 0) {
        return 1;
    }

    int[] dp = new int[n];

    for (int i = 0; i < m; i ++) {
        for (int j = 0; j < n; j ++) {
            if (i == 0 && j == 0) dp[j] = 1;
            else if (i == 0) dp[j] = 1;
            else if (j == 0) dp[j] = 1;
            else dp[j] = dp[j] + dp[j - 1];
        }
    }

    return dp[n - 1];
}

// 3. 额外一维空间，虚拟下标
public int uniquePaths(int m, int n) {
    if (n == 0) return 1;

    int[] dp = new int[n + 1];
    dp[0] = 0;
    for (int j = 1; j < n; j ++)
        dp[j] = 1;

    for (int i = 1; i < m; i ++)
        for (int j = 1; j <= n; j ++)
            dp[j] = dp[j] + dp[j - 1];
    
    return dp[n];
}

// 4. 递归，辅助方法，自顶向下
HashMap<String, Integer> map = new HashMap<>();
public int uniquePaths(int m, int n) {
    if (n == 0) return 1;
    return recursion(m - 1, n - 1);
}

private int recursion(int m, int n) {
    if (m == 0 || n == 0) return 1;

    String key = m + "-" + n;
    if (map.containsKey(key)) return map.get(key);

    int left = recursion(m - 1, n);
    int up = recursion(m, n - 1);
    int res = left + up;
    map.put(key, res);

    return res;
}

// 5. 递归，原地，自顶向下
public int uniquePaths(int m, int n) {
    if (n == 0) return 1;
    if (m == 1 || n == 1) return 1;

    String key = m + "-" + n;
    if (map.containsKey(key)) return map.get(key);

    int left = uniquePaths(m, n - 1);
    int up = uniquePaths(m - 1, n);
    int res = left + up;
    map.put(key, res);

    return res;
}

// 6. 递归，辅助方法，自底向上
public int uniquePaths(int m, int n) {
    if (n == 0) return 1;
    return recursion(0, 0, m, n);
}

private int recursion(int i, int j, int m, int n) {
    if (i == m - 1 || j == n - 1) return 1;

    String key = i + "-" + j;
    if (map.containsKey(ley)) return map.get(key);

    int right = recursion(i, j - 1, m, n);
    int down = recursion(i - 1, j, m, n);
    int res = right + down;
    map.put(key, res);

    return res;
}

```

2.[63. 不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/)
```java
// 1.二维额外空间动态规划
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    if (obstacleGrid.length == 0 || obstacleGrid[0][0] == 1) return 0;

    int[][] dp = new int[obstacleGrid.length][obstacleGrid[0].length];
    dp[0][0] = 1;
    for (int i = 1; i < obstacleGrid.length; i++) {
        if (obstacleGrid[i][0] == 1) dp[i][0] = 0;
        else dp[i][0] = dp[i - 1][0];
    }
    for (int j = 1; j < obstacleGrid[0].length; j ++) {
        if (obstacleGrid[0][j] == 1) dp[0][j] = 0;
        else dp[0][j] = dp[0][j - 1];
    }

    for (int i = 1; i < obstacleGrid.length; i ++) {
        for (int j = 1; j <obstacleGrid[0].length; j ++) {
            if (obstacleGrid[i][j] == 1) {
                dp[i][j] = 0;
            } else {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
    }

    return dp[obstacleGrid.length - 1][obstacleGrid[0].length - 1];
}

// 2. 额外二维空间，初始化 行
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    if (obstacleGrid.length == 0 || obstacleGrid[0][0] == 1) return 0;

    int[][] dp = new int[onstacleGrid.length][obstacleGrid[0].length];
    dp[0][0] = 1;
    
    for (int j = 1; j < obstacleGrid.length; j ++) {
        if (obstacleGrid[0][j] == 1) dp[0][j] = 0;
        else dp[0][j] = dp[0][j - 1];
    }

    for (int i = 1; i < obstacleGrid.length; i ++) {
        for (int j = 0; j < obstacleGrid[0].length; j ++) {
            if (obstacleGrid[i][j] == 1) dp[i][j] = 0;
            else if (j == 0) dp[i][j] = dp[i - 1][j];
            else dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }
    }

    return dp[obstacleGrid.length - 1][obstacleGrid[0].length - 1];
}

// 3. 一维额外空间动态规划
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    if (obstacleGrid.length == 0 || obstacleGrid[0][0] == 1) return 0;

    int[] dp = new int[obstacleGrid[0].length];
    dp[0] = 1;
    for (int j = 1; j < obstacleGrid[0].length; j ++) {
        if (obstacleGrid[0][j] == 1) dp[j] = 0;
        else dp[j] = dp[j - 1];
    }

    for (int i = 1; i < obstacleGrid.length; i ++) {
        for (int j = 0; j <obstacleGrid[0].length; j ++) {
            if (obstacleGrid[i][j] == 1) dp[j] = 0;
            else if (j == 0) continue;
            else dp[j] = dp[j] + dp[j - 1];
        }
    }

    return dp[obstacleGrid[0].length - 1];
}

// 4. 递归，自顶向下

public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    if (obstacleGrid.length == 0 || obstacleGrid[0][0] == 1) return 0;

    int[][] memory = new int[obstacleGrid.length][obstacleGrid[0].length];
    for (int i = 0; i < obstacleGrid.length; i ++)
        for (int j = 0; j < obstacleGrid[0].length; j ++)
            memory[i][j] = -1;

    return recursion(obstacleGrid.length - 1, obstacleGrid[0].length - 1, obstacleGrid, memory);
}

private int recursion(int m, int n, int[][] obstacleGrid, int[][] memory) {
    if (m == 0 && n == 0 && obstacleGrid[m][n] == 0) return 1;
    
    if (memory[m][n] > 0) return memory[m][n];
    
    int res = 0;
    if (m == 0) {
        if (obstacleGrid[m][n] == 1) res = 0;
        else res = recursion(m, n - 1, obstacleGrid, memory);
        memory[m][n] = res;

        return res;
    }

    if (n == 0) {
        if (obstacleGrid[m][n] == 1) res = 0;
        else res = recursion(m - 1, n, obstacleGrid, memory);
        memory[m][n] = res;
        
        return res;
    }

    if (obstacleGrid[m][n] == 1) res = 0;
    else res = recursion(m - 1, n, obstacleGrid, memory) + recursion(m, n - 1, obstacleGrid, memory);
    memory[m][n] = res;

    return res;

}

// 5. 递归，自底向上
HashMap<String, Integer> map = new HashMap<>();
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    if (obstacleGrid.length == 0 || obstacleGrid[0].length == 1) return 0;

    return recursion(0, 0, obstacleGrid);
}

private int recursion(int r, int c, int[][] obstacleGrid) {
    if (r == obstacleGrid.length - 1 && c == obstacleGrid[0].length - 1 && obstacleGrid[r][c] == 0) return 1;

    String key = r + "-" c;
    if (map.containKeys(key)) return map.get(key);

    int res;
    if (obstacleGrid[r][c] == 1) {
        res = 0;
        map.put(key, res);
        return res;
    }

    if (r == obstacleGrid.length - 1) {
        res = recursion(r, c + 1, obstacleGrid);
        map.put(key, res);
        return res;
    }

    res = recursion(r + 1, c, obstacleGrid) + recursion(r, c + 1, obstacleGrid);
    map.put(key, res);

    return res;
}


// 6. dfs + divide + memory
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    if (obstacleGrid.length == 0 || obstacleGrid[0][0] == 1) return 0;

    int[][] memo = new int[obstacelGrid.length][obstacleGrid[0].length];
    for (int i = 0; i < obstacleGrid.length; i ++) 
        for (int j = 0; j < obstacleGrid[0].length; j ++)
            memo[i][j] = -1;

    return divideDfsMemory(obstacleGrid, 0, 0, memo);
}

private int divideDfsMemory(int[][] obstacleGrid, int r, int c, int[][] memo) {
    if (r == obstacleGrid.length - 1 && c == obstacleGrid[0].length - 1 && obstacleGrid[r][c] == 0) return 1;
    if (r >= obstacleGrid.length || c >= obstacleGrid[0].length || obstacleGrid[r][c] == 1) return 0;
    if (memo[r][c] > -1) return memo[r][c];

    int sum = 0;
    sum += divideDfsMemory(obstacleGrid, r + 1, c, memo);
    sum += divideDfsMemory(obstacleGrid, r, c + 1, memo);
    memo[r][c] = sum;

    return sum;
}

// 4. 递归，自顶向下
执行用时：15 ms, 在所有 Java 提交中击败了 29.93% 的用户
内存消耗：38.4 MB, 在所有 Java 提交中击败了 10.70% 的用户
// 5. 递归，自底向上
执行用时：10 ms, 在所有 Java 提交中击败了 29.93% 的用户
内存消耗：38.6 MB, 在所有 Java 提交中击败了 5.16% 的用户
// 6. dfs 分治 记忆化搜索
执行用时：5 ms, 在所有 Java 提交中击败了 29.93% 的用户
内存消耗：37.6 MB, 在所有 Java 提交中击败了 59.80% 的用户

```

3.[980. 不同路径 III](https://leetcode-cn.com/problems/unique-paths-iii/)
```java
public int uniquePathsIII(int[][] grid) {
    int r = 0;
    int c = 0;
    int stepMax = 1;

    for (int i = 0; i < grid.length; i ++) {
        for (int j = 0; j < grid[0].length; j ++ {
            if (grid[i][j] == 1) {
                r = i;
                c = j;
                continue;
            }
            if (grid[i][j] == 0) stepMax ++;
        }
    }

    return recursion(r, c, stepMax, grid);
}

private int recursion(int r, int c, int stepMax, grid) {
    if (r < 0 || r >= grid.length || c < 0 || c >= grid[0].length || grid[r][c] == -1) return 0;
    if (grid[r][c] == 2) return stepMax == 0 ? 1 : 0;

    int res = 0;
    grid[r][c] = -1;
    res += recursion(r + 1, c, stepMax, grid);
    res += recursion(r - 1, c, stepMax, grid);
    res += recursion(r, c + 1, stepMax, grid);
    res += recursion(r, c - 1, stepMax, grid);
    grid[r][c] = 0;

    return res;
}
```

4.[509. 斐波那契数](https://leetcode-cn.com/problems/fibonacci-number/)
```java
// 1. 动态规划
public int fib(int N) {
    if (N < 2) return N;

    int[] dp = new int[N + 1];
    dp[0] = 0;
    dp[1] = 1;

    for (int i = 2; i <= N; i ++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }

    return dp[N];
}

// 2. 动态规划，记录两个状态
public int fib(int N) {
    if (N < 2) return N;

    int one = 0;
    int two = 1;
    for (int i = 2; i <= N; i ++) {
        two += one;
        one = two - one;
    }

    return two;
}

// 3. 递归，记忆化搜索
public int fib(int N) {
    int[] memory = new int[N + 1];

    return recursion(N, memory);
}

private int recursion(int n, int[] memory) {
    if (n < 2) return n;
    if (memory[n] > 0) return memory[n];
    
    int res = recursion(n - 1, memory) + recursion(n - 2, memory);
    memory[n] = res;

    return res;
}

// 4. 递归，记忆化搜索
HashMap<Integer, Integer> map = new HashMap<>();
public int fib(int N) {
    return recursion(N);
}

private int recursion(int N) {
    if (N < 2) return N;
    if (map.containsKey(N)) return map.get(N);

    int res = recursion(N - 1) + recursion(N - 2);
    map.put(N, res);

    return res;
}
```

5.[1143. 最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/)
```java

// 1. 额外二维空间，动态规划
public int longestCommonSubsequence(String text1, String text2) {
    if (text1.length() == 0 || text2.length() == 0) return 0;

    int[][] dp = new int[text1.length() + 1][text2.length() + 1];
    for (int i = 0; i < text1.length(); i ++) {
        for (int j = 0; j < text2.length(); j ++) {
            if (text1.charAt(i) == text2.charAt(j)) dp[i + 1][j + 1] = dp[i][j] + 1;
            else Math.max(dp[i + 1][j], dp[i][j + 1]);
        }
    }

    return dp[text1.length()][text2.length()];
}

执行用时：13 ms, 在所有 Java 提交中击败了 43.21% 的用户
内存消耗：42.4 MB, 在所有 Java 提交中击败了 59.77% 的用户

// 2. 额外二维空间，动态规划
public int longestCommonSubsequence(String text1, String text2) {
    if (text1.length() == 0 || text2.length() == 0) return 0;

    int[][] dp = new int[text1.length()][text2.length()];
    dp[0][0] = text1.charAt(0) == text2.charAt(0) ? 1 : 0;
    for (int i = 1; i < text1.length(); i ++) {
        if (text2.charAt(0) == text1.charAt(i)) dp[i][0] = 1;
        else dp[i][0] = dp[i - 1][0];
    }

    for (int j = 1; j < text2.length; j ++) {
        if (text1.charAt(0) == text2.charAt(j)) dp[0][j] = 1;
        else dp[0][j] = dp[0][j - 1];
    }

    for (int i = 1; i < text1.length(); i ++) {
        for (int j = 1; j < text2.length(); j ++) {
            if (text1.charAt(i) == text2.charAt(j)) dp[i][j] = dp[i - 1][j - 1] + 1;
            else dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
        }
    }

    return dp[text1.length() - 1][text2.length() - 1];
}

执行用时：13 ms, 在所有 Java 提交中击败了 43.21% 的用户
内存消耗：42.4 MB, 在所有 Java 提交中击败了 52.66% 的用户

// 3. 额外一维空间，动态规划
public int longestCommonSubsequence(String text1, String text2) {
    if (text1.length() == 0 || text2.length() == 0) return 0;

    int[] dp = new int[text2.length() + 1];
    int up = 0;
    int leftUp = 0;
    
    for (int i = 1; i <= text1.length(); i ++) {
        leftUp = 0;
        for (int j = 1; j <= text2.length(); j ++) {
            up = dp[j];
            if (text1.charAt(i - 1) == text2.charAt(j - 1)) dp[j] = leftUp + 1;
            else dp[j] = Math.max(dp[j], dp[j - 1]);
            leftUp = up;
        }
    }

    return dp[text2.length()];
}

执行用时：12 ms, 在所有 Java 提交中击败了 73.64% 的用户
内存消耗：36.4 MB, 在所有 Java 提交中击败了 99.60% 的用户

// 4. 递归，记忆化搜索
public int longestCommonSubsequence(String text1, String text2) {
    int[][] memory = new int[text1.length()][text2.length()];
    for (int i = 0; i < text1.length(); i ++) {
        for (int j = 0; j < text2.length(); j ++) 
            memory[i][j] = -1;
    }

    return recursion(0, 0, text1, text2, memory);
}

private int recursion(int i, int j, String text1, String text2, int[][] memory) {
    if (i == text1.length() || j == text2.length()) return 0;

    if (memory[i][j] > - 1) return memory[i][j];
    int res;

    if (text1.charAt(i) == text2.charAt(j)) {
        res = recursion(i + 1, j + 1, text1, text2, memory);
    } else {
        res = Math.max(recursion(i + 1, j, text1, text2, memory), recursion(i, j + 1, text1, text2, memory));
    }

    memory[i][j] = res;

    return res;
}


执行用时：22 ms, 在所有 Java 提交中击败了 5.70% 的用户
内存消耗：42.7 MB, 在所有 Java 提交中击败了 9.01% 的用户
```

6.[70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/description/)
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

7.[120. 三角形最小路径和](https://leetcode-cn.com/problems/triangle/description/) [三角形最小路径和高票回答-国际站-python](https://leetcode.com/problems/triangle/discuss/38735/Python-easy-to-understand-solutions-(top-down-bottom-up))
```java
// 1. 递归 记忆化搜索
public int minimumTotal(List<List<Integer>> triangle) {
    int col = triangle.get(triangle.size() - 1).size();
    int[][] memory = new int[triangle.size()][col];
    for (int i = 0; i < triangle.size(); i ++) {
        for (int j = 0; j < col; j ++) 
            memory[i][j] = Integer.MIN_VALUE;
    }

    return recursion(0, 0, triangle, memory);
}

private int recursion(int level, int index,List<List<Integer>> triangle, int[][] memory) {
    if (level == triangle.size()) return 0;

    if (memory[level][index] > Integer.MIN_VALUE) return memory[level][index];

    int origin = recursion(level + 1, index, triangle, memory);
    int next = recursion(level + 1, index + 1, triangle, memory);
    int res = triangle.get(level).get(index) + Math.min(origin, next);
    memory[level][index] = res;

    return res;
}

执行用时：1 ms, 在所有 Java 提交中击败了 99.77% 的用户
内存消耗：38.6 MB, 在所有 Java 提交中击败了 95.96% 的用户

// 2. 额外二维空间动态规划
public int minimumTotal(List<List<Integer>> triangle) {
    int n = triangle.size();

    int[][] dp = new int[n][n];
    dp[0][0] = triangle.get(0).get(0);
    for (int i = 1; i < n; i ++) {
        dp[i][0] = dp[i - 1][0] + triangle.get(i).get(0);
        for (int j = 1; j < i; j ++) {
            dp[i][j] = Math.min(dp[i - 1][j - 1], dp[i - 1][j]) + triangle.get(i).get(j);
        }
        dp[i][i] = dp[i - 1][i - 1] + triangle.get(i).get(i);
    }

    int min = dp[n - 1][0];
    for (int i = 1; i < n; i ++) {
        min = Math.min(min, dp[n - 1][i]);
    }

    return min;
}

执行用时：3 ms, 在所有 Java 提交中击败了 74.32% 的用户
内存消耗：38.4 MB, 在所有 Java 提交中击败了 99.30% 的用户

// 3. 额外一维空间，动态规划，自顶向下
public int minimumTotal(List<List<Integer>> triangle) {
    if (triangle == null || triangle.size() == 0) return 0;

    int n = triangle.size();
    int[] dp = new int[n];

    for (int j = 0; j < n; j ++) 
        dp[j] = triangle.get(n - 1).get(j);
    

    for (int i = n - 2; i >= 0; i --) 
        for (int j = 0; j < = i; j ++)
            dp[j] = Math.min(dp[j], dp[j + 1]) + triangle.get(i).get(j);

    return dp[0];
}


执行用时：2 ms ,在所有 Java 提交中击败了 95.21% 的用户
内存消耗：38.7 MB, 在所有 Java 提交中击败了 93.02% 的用户

// 4. 额外一维空间，动态规划，自底向上
public int minimumTotal(List<List<Integer>> triangle) {
    if (triangle == null || triangle.size() == 0) return 0;

    int n = triangle.size();
    int[] dp = new int[n];
    int leftUp = 0;
    int end = 0;
    int tmp = 0;

    for (int i = 1; i < n; i ++) {
        end = dp[i];

        dp[0] = dp[0] + triangle.get(i).get(0);
        for (int j = 1; j < i; j ++) {
            tmp = dp[j];
            dp[j] = Math.min(dp[j], dp[j - 1]) + triangle.get(i).get(j);
            leftUp = tmp;
        }
        dp[0] = end + triangle.get(i).get(i);
    }

    int min = dp[0];
    for (int j = 1; j < n; j ++)
        min = Math.min(min, dp[j]);

    return min;
}

```




```python
# O(n*n/2) space, top-down 
def minimumTotal1(self, triangle):
    if not triangle:
        return 
    res = [[0 for i in xrange(len(row))] for row in triangle]
    res[0][0] = triangle[0][0]
    for i in xrange(1, len(triangle)):
        for j in xrange(len(triangle[i])):
            if j == 0:
                res[i][j] = res[i-1][j] + triangle[i][j]
            elif j == len(triangle[i])-1:
                res[i][j] = res[i-1][j-1] + triangle[i][j]
            else:
                res[i][j] = min(res[i-1][j-1], res[i-1][j]) + triangle[i][j]
    return min(res[-1])
    
# Modify the original triangle, top-down
def minimumTotal2(self, triangle):
    if not triangle:
        return 
    for i in xrange(1, len(triangle)):
        for j in xrange(len(triangle[i])):
            if j == 0:
                triangle[i][j] += triangle[i-1][j]
            elif j == len(triangle[i])-1:
                triangle[i][j] += triangle[i-1][j-1]
            else:
                triangle[i][j] += min(triangle[i-1][j-1], triangle[i-1][j])
    return min(triangle[-1])
    
# Modify the original triangle, bottom-up
def minimumTotal3(self, triangle):
    if not triangle:
        return 
    for i in xrange(len(triangle)-2, -1, -1):
        for j in xrange(len(triangle[i])):
            triangle[i][j] += min(triangle[i+1][j], triangle[i+1][j+1])
    return triangle[0][0]

# bottom-up, O(n) space
def minimumTotal(self, triangle):
    if not triangle:
        return 
    res = triangle[-1]
    for i in xrange(len(triangle)-2, -1, -1):
        for j in xrange(len(triangle[i])):
            res[j] = min(res[j], res[j+1]) + triangle[i][j]
    return res[0]

```

8.[53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)
```java
// 1. 动态规划
public int maxSubArray(int[] nums) {
    int max = nums[0];
    for (int i = 1; i < nums.length; i ++) {
        if (nums[i - 1] > 0) nums[i] += nums[i - 1];
        max = Math.max(max, nums[i]);
    }

    return max;
}

// 2. 贪心
public int maxSubArray(int[] nums) {
    int pre = 0;
    int max = nums[0];
    for (int num: nums) {
        pre = Math.max(pre, pre + num);
        max = Math.max(pre, max);
    }

    return max;
}

// 3. 分治
public int maxSubArray(int[] nums) {

}
```

9.[152. 乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/description/)
```java

```

10.[322. 零钱兑换](https://leetcode-cn.com/problems/coin-change/description/)
```java

```

11.[198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/)
```java

// 1. 动态规划，自底向上，空间O(n)
public int rob(int[] nums) {
    if (nums.length == 0) return 0;
    if (nums.length == 1) return nums[1];

    int[] dp = new int[nums.length];
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]);

    for (int i = 2; i < nums.length; i ++) {
        dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
    }

    return dp[nums.length - 1];
}

// 2. 动态规划，自底向上，空间O(1)
public int rob(int[] nums) {
    if (nums.length == 0) return 0;
    if (nums.length == 1) return nums[0];

    int dp1 = nums[0];
    int dp2 = Math.max(num[0], nums[1]);
    int tmp = 0;
    for (int i = 2; i < nums.length; i ++) {
        tmp = dp2;
        dp2 = Math.max(dp2, dp1 + nums[i]);
        dp1 = tmp;
    }

    return dp2;
}

// 3. 动态规划，自顶向下，虚拟房源，O(N)
public int rob(int[] nums) {
    if (nums.length == 0) return 0;
    if (nums.length == 1) return nums[0];

    int[] dp = new int[nums.length + 2];
    dp[nums.length + 1] = 0;
    dp[nums.length] = 0;

    for (int i = nums.length - 1; i >=0; i --) {
        dp[i] = Math.max(dp[i + 1], dp[i + 2] + nums[i]);
    }

    return dp[0];
}

// 4. 动态规划，自顶向下，虚拟房源，O(1)
public int rob(int[] nums) {
    if (nums.length == 0) return 0;
    if (nums.length == 1) return nums[0];

    int dp1 = 0;
    int dp2 = 0;
    int max = 0;
    for (int i = nums.length - 1; i >= 0; i ++) {
        max = Math.max(dp1, dp2 + nums[i]);
        dp2 = dp1;
        dp1 = max;
    }

    return max;
}

// 5. dfs + memory
Map<Integer, Integer> map = new HashMap<>();
public int rob(int[] nums) {
    if (nums.length == 0) return 0;

    return dfs(nums, 0);
}

private int dfs(int[] nums, int start) {
    if (start >= nums.length) return 0;
    if (map.containsKey(start)) return map.get(start);

    int res = Math.max(dfs(nums, start + 1, dfs(nums, start + 2) + nums[start]));
    map.put(start, res);

    return res;
}

// 6. dfs + memory
public int rob(int[] nums) {
    if (nums.length == 0) return 0;
    if (nums.length == 1) return nums[0];

    int[] memory = new int[nums.length];
    for (int i = 0; i < nums.length; i ++)
        memory[i] = -1;

    return dfs(0, nums, memory);
}

private int dfs(int start, int[] nums, int[] memory) {
    if (start >= nums.length) return 0;
    if (memory[start] > 0) return memory[start];

    int res = Math.max(dfs(start + 1, nums, memory), dfs(start + 2, nums, memory) + nums[start]);
    memory[start] = res;

    return res;
}


```

12.[213. 打家劫舍 II](https://leetcode-cn.com/problems/house-robber-ii/description/)
```java

```

13.[121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/#/description)
```java

```

14.[122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)
```java

```

15.[123. 买卖股票的最佳时机 III](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)
```java

```

16.[309. 最佳买卖股票时机含冷冻期](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)
```java

```

17.[188. 买卖股票的最佳时机 IV](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/)
```java

```

18.[714. 买卖股票的最佳时机含手续费](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)
```java

```

(一个方法团灭 6 道股票问题)[https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/solution/yi-ge-fang-fa-tuan-mie-6-dao-gu-piao-wen-ti-by-l-3/]

19.[55. 跳跃游戏](https://leetcode-cn.com/problems/jump-game/)
```java

```

20.[45. 跳跃游戏 II](https://leetcode-cn.com/problems/jump-game-ii/)
```java

```

21.[518. 零钱兑换 II](https://leetcode-cn.com/problems/coin-change-2/)
```java

```

22.[279. 完全平方数](https://leetcode-cn.com/problems/perfect-squares/)
```java

```

23.[72. 编辑距离](https://leetcode-cn.com/problems/edit-distance/)
```java

```

24.[64. 最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)
```java

// 1. 额外二维空间动态规划
public int minPathSum(int[][] grid) {
    if (grid.length == 0) {
        return 0;
    }

    int[][] dp = new int[grid.length][grid[0].length];
    dp[0][0] = grid[0][0];

    for (int i = 1; i < grid.length; i ++) dp[i][0] = grid[i][0] + dp[i - 1][0];
    for (int i = 1; i < grid[0].length; i ++) dp[0][i] = grid[0][i] + dp[0][i - 1];

    for (int i = 1; i < grid.length; i ++) {
        for (int j = 1; j < grid[0].length; j ++) {
            dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
        }
    }

    return dp[grid.length - 1][grid[0].length - 1];
}


// 2. 原地二维空间动态规划
public int minPathSum(int[][] grid) {
    if (grid.length == 0) {
        return 0;
    }

    for (int i = 1; i < grid.length; i ++) grid[i][0] = grid[i][0] + grid[i - 1][0];
    for (int i = 1; i < grid[0].length; i ++) grid[0][i] = grid[0][i] + grid[0][i - 1];

    for (int i = 1; i < grid.length; i ++) {
        for (int j = 1; j < grid[0].length; j ++) {
            grid[i][j] = Math.min(grid[i - 1][j], grid[i][j - 1]) + grid[i][j];
        }
    }

    return grid[grid.length - 1][grid[0].length - 1];
}

// 3. 额外一维空间动态规划
public int minPathSum(int[][] grid) {
    if (grid.length == 0) {
        return 0;
    }

    int[] dp = new int[grid[0].length];

    for (int i = 0; i < grid.length; i ++) {
        for (int j = 0; j < grid[0].length; j ++) {
            // 初始化 [0][0] 格子
            if (i == 0 && j == 0) dp[j] = grid[i][j];
            // 第 0 行格子，从前到后一次累加上个格子的值
            else if (i == 0) dp[j] = dp[j - 1] + grid[i][j];
            // 从上一个格子到当前格子，因此，路径上的数字和 = 上一个格子 + 当前格子
            else if (j == 0) dp[j] = dp[j] + grid[i][j];
            // dp[j] 格子上方   dp[j-1] 格子前方
            else dp[j] = Math.min(dp[j], dp[j - 1]) + grid[i][j];
        }
    }

    return dp[dp.length - 1];
}

// 4. 额外一维空间优化 if else
public int minPathSum(int[][] grid) {
    if (grid.length == 0) {
        return 0;
    }

    int[] dp = new int[grid[0].length];
    dp[0] = grid[0][0];
    for (int i = 1; i < grid[0].length; i ++) dp[i] = dp[i - 1] + grid[0][i];

    for (int i = 1; i < grid.length; i ++) {
        for (int j = 0; j < grid[0.length; j ++) {
            if (j == 0) dp[j] = dp[j] + grid[i][j];
            else dp[j] = Math.min(dp[j], dp[j - 1]) + grid[i][j];
        }
    }

    return dp[grid[0].length - 1];
}

// 5. 递归 + 分治 + 记忆化搜索
private int M;
private int N;
private int[][] memory;
public int minPathSum(int[][] grid) {
    if (grid.length == 0) return 0;
    M = grid.length;
    N = grid[0].length;
    memory = new int[M][N];

    for (int i = 0; i < M; i ++) {
        for (int j = 0; j < N; j ++) {
            memory[i][j] = -1;
        }
    }

    return recursion(grid, 0, 0);
}

private int recursion(int[][] grid, int r, int c) {
    if (r < 0 || r >= M || c < 0 || c >= N) return Integer.MAX_VALUE;
    if (memory[r][c] > -1) return memory[r][c];
    if (r == M - 1 && c == N - 1) return grid[M - 1][N - 1];

    int right = recursion(grid, r, c + 1);
    int down = recursion(grid, r + 1, c);
    int res = Math.min(right, down) + grid[r][c];
    memory[r][c] = res;

    return res;
}
```

25.[91. 解码方法](https://leetcode-cn.com/problems/decode-ways/)
```java
// 1. 一维动态规划，记录行状态
public int numDecodings(String s) {
    if (s.length() == 0) {
        return 0;
    }

    int[] dp = new int[s.length() + 1];
    dp[s.length()] = 1;
    if (s.charAt(s.length() - 1) == '0') dp[s.length() - 1] = 0;
    else dp[s.length() - 1] = 1;

    for (int i = s.length() - 2; i >= 0; i --) {
        if (s.charAt(i) == '0') {
            dp[i] = 0;
            continue;
        }

        if ((s.charAt(i) - '0') * 10 + (s.charAt(i + 1) - '0') <= 26) dp[i] = dp[i + 1] + dp[i + 2];
        else dp[i] = dp[i + 1];
    }

    return dp[0];
}
```

26.[221. 最大正方形](https://leetcode-cn.com/problems/maximal-square/)
```java

```

27.[621. 任务调度器](https://leetcode-cn.com/problems/task-scheduler/)
```java

```

28.[647. 回文子串](https://leetcode-cn.com/problems/palindromic-substrings/)
```java

```

29.[32. 最长有效括号](https://leetcode-cn.com/problems/longest-valid-parentheses/)
```java

```

30.[363. 矩形区域不超过 K 的最大数值和](https://leetcode-cn.com/problems/max-sum-of-rectangle-no-larger-than-k/)
```java

```

31.[403. 青蛙过河](https://leetcode-cn.com/problems/frog-jump/)
```java

```

32.[410. 分割数组的最大值](https://leetcode-cn.com/problems/split-array-largest-sum/)
```java

```

33.[552. 学生出勤记录 II](https://leetcode-cn.com/problems/student-attendance-record-ii/)
```java

```

34.[76. 最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/)
```java

```

35.[312. 戳气球](https://leetcode-cn.com/problems/burst-balloons/)
```java

```

36.[208. 实现 Trie (前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/#/description)
```java

```

37.[212. 单词搜索 II](https://leetcode-cn.com/problems/word-search-ii/)
```java

```

38.[200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)
```java

```

39.[36. 有效的数独](https://leetcode-cn.com/problems/valid-sudoku/description/)
```java

```

40.[51. N 皇后](https://leetcode-cn.com/problems/n-queens/)
```java

```

41.[127. 单词接龙](https://leetcode-cn.com/problems/word-ladder/)
```java

```

42.[1091. 二进制矩阵中的最短路径](https://leetcode-cn.com/problems/shortest-path-in-binary-matrix/)
```java

```

.[]()
```java

```

.[]()
```java

```