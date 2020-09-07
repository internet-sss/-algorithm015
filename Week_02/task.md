1. HashMap 的小总结
```java

```

[2. 有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/description/)
```java
（亚马逊、Facebook、谷歌在半年内面试中考过）

// 1. 枚举
// 2. Hash
// 3. 另类 Hash,arr

// 3. arr
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) {
        return false;
    }

    int[] arr = new int[26];
    for (int i = 0; i < s.length(); i ++) {
        arr[s.charAt(i) - 'a'] ++;
        arr[t.charAt(i) - 'a'] --;
    }

    for (int i = 0; i < 26; i ++) {
        if (arr[i] != 0) {
            return false;
        }
    }

    return true;
}
```

[3. 两数之和](https://leetcode-cn.com/problems/two-sum/description/)
```java
（近半年内，亚马逊考查此题达到 216 次、字节跳动 147 次、谷歌 104 次，Facebook、苹果、微软、腾讯也在近半年内面试常考）
// 1.暴力
// 2.Hash

// 2.Hash
public int[] twoSum(int[] nums, int target) {
    if (nums.length < 2) {
        return new int[] {};
    }

    HashMap<Integer, Integer> map = new HashMap<>();
    
    for (int i = 0; i < nums.length; i ++) {
        if (map.containsKey(nums[i])) {
            return new int[] {i, map.get(nums[i])};
        } else {
            map.put(target - nums[i], i);
        }
    }

    throw new IllegalArgumentException("No two sum solution");
}

// 1.暴力
public int[] twoSum(int[] nums, int target) {
    if (nums.length < 2) {
        return new int[] {};
    }

    // 1.暴力
    for (int i = 0; i < nums.length - 1; i ++) {
        for (int j = i + 1; j < nums.length; j ++) {
            if (nums[i] + nums[j] == target) {
                return new int[] {i, j};
            }
        }
    }

    throw new IllegalArgumentException("No two sum solution");
}

```

[4. N 叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/description/)
```java
（亚马逊在半年内面试中考过）


```

5. [HeapSort ：自学](https://www.geeksforgeeks.org/heap-sort/)
```java

```

[6. 字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/)
```java
（亚马逊在半年内面试中常考）

```

[7. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
```java
（亚马逊、字节跳动、微软在半年内面试中考过）
private static void recursion(TreeNode root) {
    if (root == null) {
        return;
    }

    recursion(root.left);
    System.out.println(root.val);
    recursion(root.right);
}
```

[8. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)
```java
（字节跳动、谷歌、腾讯在半年内面试中考过）
private static void recursion(TreeNode root) {
    if (root == null) {
        return;
    }
    System.out.println(root.val);
    recursion(root.left);
    recursion(root.right);
}
```

[9. N 叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)
```java
（亚马逊在半年内面试中考过）

```

[10. 丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)
```java
（字节跳动在半年内面试中考过）
```

[11. 前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)
```java
（亚马逊在半年内面试中常考）
```

[12. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)
```java
public int climbStairs(int n) {
    if (n < 4) {
        return n;
    }

    int two = 2;
    int three = 3;

    for (int i = 4; i <= n; i ++) {
        three += two;
        two = three - two;
    }

    return three;
}
    
```

[13. 括号生成](https://leetcode-cn.com/problems/generate-parentheses/)
```java

```

[14. Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)
```java

```

[15. 子集](https://leetcode-cn.com/problems/subsets/)
```java

```

[16. N 皇后](https://leetcode-cn.com/problems/n-queens/)
```java
public List<List<String>> solveNQueens(int n) {

    List<List<String>> res = new ArrayList<>();
    HashSet<Integer> col = new HashSet<>();
    HashSet<Integer> d1 = new HashSet<>();
    HashSet<Integer> d2 = new HashSet<>();
    int[] queens = new int[n];
    int row = 0;
    
    recursion(res, queens, n, 0, col, d1, d2);

    return res;
}

private void recursion(List<List<String>> res, int[] queens, int n, int row, 
        HashSet<Integer> col, HashSet<Integer> d1, HashSet<Integer> d2) {
            
    if (row == n) {
        List<String> tmp = generate(queens, n);
        res.add(tmp);
    } else {
        for (int i = 0; i < n; i ++) {
            if (col.contains(i)) {
                continue;
            }

            if (d1.contains(row - i)) {
                continue;
            }

            if (d2.contains(row + i)) {
                continue;
            }

            queens[row] = i;
            col.add(i);
            d1.add(row - i);
            d2.add(row + i);
            recursion(res, queens, n, row + 1, col, d1, d2);
            queens[row] = -1;
            col.remove(i);
            d1.remove(row - i);
            d2.remove(row + i);
        }
    }
}

private List<String> generate(int[] queens, int n) {
    List<String> board = new ArrayList<String>();
    for (int i = 0; i < n; i++) {
        char[] row = new char[n];
        Arrays.fill(row, '.');
        row[queens[i]] = 'Q';
        board.add(new String(row));
    }
    return board;
}
```