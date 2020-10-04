1.[62. 不同路径](https://leetcode-cn.com/problems/unique-paths/)
```java
// 1. 额外二维空间动态规划
public int uniquePaths(int m, int n) {
    if (m == 0 && n == 0) {
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
    if (m == 0 && n == 0) {
        return 0;
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

// 2. 一维额外空间动态规划
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

// 3. dfs + divide + memory
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

```

3.[980. 不同路径 III](https://leetcode-cn.com/problems/unique-paths-iii/)
```java

```

4.[509. 斐波那契数](https://leetcode-cn.com/problems/fibonacci-number/)
```java

```

5.[1143. 最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/)
```java

```

6.[70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/description/)
```java

```

7.[120. 三角形最小路径和](https://leetcode-cn.com/problems/triangle/description/) [三角形最小路径和高票回答-国际站-python](https://leetcode.com/problems/triangle/discuss/38735/Python-easy-to-understand-solutions-(top-down-bottom-up))
```java

```

8.[53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)
```java

```

9.[152. 乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/description/)
```java

```

10.[322. 零钱兑换](https://leetcode-cn.com/problems/coin-change/description/)
```java

```

11.[198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/)
```java

// dfs + memory
Map<Integer, Integer> map = new HashMap<>();
public int rob(int[] nums) {
    if (nums.length == 0) return 0;

    return Math.max(dfs(nums, 0), dfs(nums, 1));
}

private int dfs(int[] nums, int start) {
    if (start >= nums.length) return 0;
    if (map.containsKey(start)) return map.get(start);

    int res = Math.max(dfs(nums, start + 1, dfs(nums, start + 2) + nums[start]));
    map.put(start, res);

    return res;
}

// 自底向上，虚拟房源，额外空间 O(n)
public int rob(int[] nums) {
    if (nums.length == 0) return 0;
    int[] dp = new int[nums.length + 2];
    dp[nums.length + 1] = 0;
    dp[nums.length] = 0;

    for (int i = nums.length - 1; i >= 0; i --) {
        dp[i] = Math.max(dp[i + 1], dp[i + 2] + nums[i]);
    }

    return dp[0];
}

// 自底向上，虚拟房源，额外空间 O(1)
public int rob(int[] nums) {
    int res = 0;
    int dp_i_1 = 0;
    int dp_i_2 = 0;

    for (int i = nums.length - 1; i >= 0; i --) {
        res = Math.max(dp_i_1, dp_i_2 + nums[i]);
        dp_i_2 = dp_i_1;
        dp_i_1 = res;
    }

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