
1.[191. 位1的个数](https://leetcode-cn.com/problems/number-of-1-bits/)
```java
public int hammingWeight(int n) {
    int sum = 0;
    while (n != 0) {
        sum ++;
        n &= n - 1;
    }
    return sum;
}
```

2.[231. 2的幂](https://leetcode-cn.com/problems/power-of-two/)
```java

```

3.[190. 颠倒二进制位](https://leetcode-cn.com/problems/reverse-bits/)
```java

```

4.[51. N 皇后](https://leetcode-cn.com/problems/n-queens/description/)
```java
// 1. 递归 + 回溯，列、撇、捺存储已经遍历过的元素
public List<List<String>> solveNQueens(int n) {
    List<List<String>> res = new ArrayList<>();
    if (n < 1) return res;

    int[] queens = new int[n];
    Set<Integer> cols = new HashSet<>();
    Set<Integer> pie = new HashSet<>();
    Set<Integer> na = new HashSet<>();

    dfs(0, cols, pie, na, res, queens);
    return res;
}

private void dfs(int row, Set<Integer> cols, Set<Integer> pie, Set<Integer> na, List<List<String>> res, int[] queens) {
    if (row == queens.length) {
        res.add(generate(queens));
        return;
    }

    for (int col = 0; col < queens.length; col ++) {
        if (cols.contains(col)) continue;
        if (pie.contains(row + col)) continue;
        if (na.contains(row - col)) continue;

        queens[row] = i;
        cols.add(col);
        pie.add(row + col);
        na.add(row - col);

        dfs(row + 1, cols, pie, na, res, queens);

        cols.remove(col);
        pie.remove(row + col);
        na.remove(row - col);

    }
}

private List<String> generate(int[] queens) {
    List<String> res = new ArrayList<>();
    for (int i = 0; i < queens.length; i ++) {
        char[] tmp = new char[queens.length];
        Arrays.fill(tmp, '.');
        tmp[queens[i]] = 'Q';
        res.add(new String(tmp));
    }

    return res;
}


// 2. 直接放置皇后，检查是否可以放置
List<List<String>> res = new ArrayList<>();
int[] cols;// cols[row] = col  第几行第几列放置 Q
public List<List<String>> solveNQueens(int n) {
    if (n < 1) return res;
    cols = new int[n];
    place(0);

    return res;
}

private void place(int row) {
    if (row == cols.length) {
        generate();
        return;
    }

    for (int col = 0; col < cols.length; col ++) {
        if (isValid(row, col)) {
            cols[row] = col;
            // 回溯
            place(row + 1);
        }
    }
}

// 剪枝
private boolean isValid(int row, int col) {
    for (int i = 0; i < row; i ++) {
        if (cols[i] == col) return false;
        if (row - i == Math.abs(cols[i] - col)) return false;
    }
    return true;
}

private void generate() {
    List<String> tmp = new ArrayList<>();
    for (int row = 0; row < cols.length; row ++) {
        StringBuilder sb = new StringBuilder();
        for (int col = 0; col < cols.length; col ++) {
            if (cols[row] == col) sb.append('Q');
            else sb.append('.');
        }
        tmp.add(sb.toString());
    }
    res.add(tmp);
}

// 3.直接放置皇后，把检查环节换掉
int[] queens;
boolean[] cols;
boolean[] leftUp;
boolean[] rightUp;
List<List<String>> res = new ArrayList<>();
public List<List<String>> solveNQueens(int n) {
    if (n < 1) return res;

    queens = new int[n];
    cols = new boolean[n];
    leftUp = new boolean[(n << 1) - 1];
    rightUp = new boolean[leftUp.length];

    place(0);
    return res;

}

private void place(int row) {
    if (row == queens.length) {
        generate();
        return;
    }
    
    for (int col = 0; col < queens.length; col ++) {
        if (cols[col]) continue;
        int luIndex = row - col + queens.length - 1;
        if (leftUp[luIndex]) continue;
        int ruIndex = row + col;
        if (rightUp[ruIndex]) continue;
 
        queens[row] = col;
        cols[col] = true;
        leftUp[luIndex] = true;
        rightUp[ruIndex] = true;
        place(row + 1);
        cols[col] = false;
        leftUp[luIndex] = false;
        rightUp[ruIndex] = false;

    }
}

private void generate() {
    List<String> tmp = new ArrayList<>();
    for (int row = 0; row < queens.length; row ++) {
        StringBuilder sb = new StringBuilder();
        for (int col = 0; col < queens.length; col ++) {
            if (queens[row] == col) sb.append('Q');
            else sb.append('.');
        }
        tmp.add(sb.toString());
    }
    res.add(tmp);
}



// 4. 位运算压缩空间，只适用于 8 皇后及以下
// 可以想到位运算：
//      1.存储的东西是 boolean
//      2.表示的二进制位不要太长

int[] queens;
int cols;
int leftUp;
int rightUp;
List<List<String>> res = new ArrayList<>();
public List<List<String>> solveNQueens(int n) {
    if (n < 1) return res;
    queens = new int[n];
    place(0);
    return res;
}

private void place(int row) {
    if (row == queens.length) {
        generate();
        return;
    }

    for (int col = 0; col < queens.length; col ++) {
        int cv = 1 << col;
        if ((cols & cv) != 0) continue;
        int lv = 1 << (row - col + queens.length - 1);
        if ((leftUp & lv) != 0) continue;
        int rv = 1 << (row + col);
        if ((rightUp & rv) != 0) continue;

        queens[row] = col;
        cols |= cv;
        leftUp |= lv;
        rightUp |= rv;
        place(row + 1);
        cols &= ~cv;
        leftUp &= ~lv;
        rightUp &= ~rv;
    }
}

private void generate() {
    List<String> tmp = new ArrayList<>();
    for (int row = 0; row < queens.length; row ++) {
        StringBuilder sb = new StringBuilder();
        for (int col = 0; col < queens.length; col ++) {
            if (queens[row] == col) sb.append('Q');
            else sb.append('.');
        }
        tmp.add(sb.toString());
    }
    res.add(tmp);
}

// 5. 位运算，简介版本
private int size;
private int count;
private void solve(int row, int ld, int rd) {
    if (row == size) {
        count++;
        return;
    }
    int pos = size & (~(row | ld | rd));
    while (pos != 0) {
        int p = pos & (-pos);
        pos -= p; // pos &= pos - 1; 
        solve(row | p, (ld | p) << 1, (rd | p) >> 1);
    }
}

public int totalNQueens(int n) {
    count = 0;
    size = (1 << n) - 1;
    solve(0, 0, 0);
    return count;
}
```

5.[52. N皇后 II](https://leetcode-cn.com/problems/n-queens-ii/description/)
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