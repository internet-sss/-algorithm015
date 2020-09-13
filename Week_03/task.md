1.[70.爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)
```java
（阿里巴巴、腾讯、字节跳动在半年内面试常考）
// 1.动态规划
// 2.矩阵快速幂
// 3.通项公式

// 1.动态规划
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

2.[22.括号生成](https://leetcode-cn.com/problems/generate-parentheses/solution/gua-hao-sheng-cheng-by-leetcode-solution/)
```java
 (字节跳动在半年内面试中考过)
 // 1.暴力
 // 2.回溯
 // 3.按括号序列长度递归

 // 2.回溯
 public List<String> generateParenthesis(int n) {
    List<String> res = new ArrayList<>();
    recursion(0, 0, n, "", res);

    return res;
}

private void recursion(int left, int right, int n, String str, List<String> res) {
    if (left == n && right == n) {
        res.add(str);
        return;
    }

    if (left < n) {
        recursion(left + 1, right, n, str + "(", res);
    }

    if (right < left) {
        recursion(left, right + 1, n, str + ")", res);
    }
}
```
3.[226.翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/description/)
```java
(谷歌、字节跳动、Facebook 在半年内面试中考过)
// 1.原地递归
// 2.迭代，DFS，栈
// 3.迭代，BFS，队列
public TreeNode invertTree(TreeNode root) {
    
    TreeNode cur = null;
    TreeNode tmp = null;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        cur = queue.poll();
        if (cur == null) {
            continue;
        }

        tmp = cur.left;
        cur.left = cur.right;
        cur.right = tmp;

        queue.offer(cur.left);
        queue.offer(cur.right);
    }

    return root;
}


// 2.迭代，DFS，栈
public TreeNode invertTree(TreeNode root) {

    TreeNode cur = null;
    TreeNode tmp = null;
    Stack<TreeNode> stack = new Stack<>();
    stack.add(root);

    while (!stack.isEmpty()) {
        cur = stack.pop();
        if (cur == null){
            continue;
        }

        tmp = cur.left;
        cur.left = cur.right;
        cur.right = tmp;

        stack.add(cur.right);
        stack.add(cur.left);
    }

    return root;
}

// 1.原地递归
public TreeNode invertTree(TreeNode root) {
    if (root == null) {
        return null;
    }

    TreeNode tmp = root.left;
    root.left = root.right;
    root.right = tmp;
    invertTree(root.left);
    invertTree(root.right);

    return root;
}
```
4.[98.验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)
```java
（亚马逊、微软、Facebook 在半年内面试中考过）
// 1.前序遍历，递归，dfs
// 2.前序遍历，栈
// 3.层序遍历，队列，广度优先
// 4.中序遍历，栈
// 5.中序遍历，递归

// 5.中序遍历，递归
long last = Long.MIN_VALUE;
public boolean isValidBST(TreeNode root) {
    if (root == null) {
        return true;
    }

    if (!isVaslidBST(root.left)) {
        return false;
    }

    if (root.val <= last) {
        return false;
    }
    last = root.val;

    if (!isValidBST(root.right)) {
        return false;
    }

    return true;
}

// 4.中序遍历，栈
public boolean isValidBST(TreeNode root) {
    Stack<TreeNode> stack = new Stack<>();
    long last = Long.MIN_VALUE;

    while (!stack.isEmpty() || root != null) {
        while (root != null) {
            stack.add(root);
            root = root.left;
        }

        root = stack.pop();
        if (root.val <= last) {
            return false;
        }
        last = root.val;

        root = root.right;
    }

    return true;
}


// 3.层序遍历，队列，广度优先
Queue<TreeNode> nodeQueue = new LinkedList<>();
Queue<Long> lowerQueue = new LinkedList<>();
Queue<Long> upperQueue = new LinkedListM<>();

public boolean isValidBST(TreeNode root) {
    long lower = Long.MIN_VALUE
    long upper = Long.MAX_VALUE;
    updateQueue(root, lower, upper);

    while (!nodeQueue.isEmpty()) {
        TreeNode cur = nodeQueue.poll();
        lower = lowerQueue.poll();
        upper = upplerQueue.poll();

        if (cur == null) {
            continue;
        }

        if (cur.val <= lower) {
            return false;
        }

        if (cur.val >= upper) {
            return false;
        }

        updateQueue(cur.left, lower, cur.val);
        updateQueue(cur.right, cur.val, upper);
    }

    return true;
}

private void updateQueue(TreeNode node, long lower, long upper) {
    nodeQueue.offer(node);
    lowerQueue.offer(lower);
    upperQueue.offer(upper);
}

// 2.前序遍历，栈
Stack<TreeNode> nodeStack = new Stack<>();
Stack<Long> lowerStack = new Stack<>();
Stack<Long> upperStack = new Stack<>();
public boolean isValidBST(TreeNode root) {
    long lower = Long.MIN_VALUE;
    long upper = Long.MAX_VALUE;
    updateStack(root, lower, upper);

    while (!nodeStack.isEmpty()) {
        TreeNode cur = nodeStack.pop();
        lower = lowerStack.pop();
        upper = upperStack.pop();

        if (cur == null) {
            continue;
        }

        if (cur.val <= lower) {
            return false;
        }

        if (cur.val >= upper) {
            return false;
        }

        updateStack(cur.left, lower, cur.val);
        updateStack(cur.right, cur.val, upper);
    }

    return true;
}

private void updateStack(TreeNode node, long lower, long upper) {
    nodeStack.add(node);
    lowerStack.add(lower);
    upperStack.add(upper);
}


// 1.前序遍历，递归，dfs
public boolean isValidBST(TreeNode root) {
    return recursion(root, Long.MIN_VALUE, Long.MAX_VALUE);
}

private boolean recursion(TreeNode root, long min, long max) {
    if (root == null) {
        return true;
    }

    if (root.val <= min) {
        return false;
    }

    if (root.val >= max) {
        return false;
    }

    if (!recursion(root.left, min, root.val)){
        return false;
    }

    if (!recursion(root.right, root.val, max)) {
        return false;
    }

    return true;
}
```
5.[104.二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)
```java
（亚马逊、微软、字节跳动在半年内面试中考过）
// 1.深度优先，递归
// 2.层序遍历，队列

// 2.层序遍历，队列
public int maxDepth(TreeNode root) {
    if (root == null) {
        return 0;
    }
    int ans = 0;
    int size = 0;
    Queue<TreeNode> queue = new LinkedList<>();

    while (!queue.isEmpty()) {
        size = queue.size(); // 当前层节点个数
        // 弹出当前层节点，并记录下一层节点
        while (size > 0) {
            TreeNode cur = queue.poll();
            if (cur.left != null) {
                queue.offer(cur.left);
            }

            if (cur.right != null) {
                queue.offer(cur.right);
            }
            size --;
        }
        ans ++;
    }

    return ans;
}

// 1. 深度优先，递归
int deep = 0;
public int maxDepth(TreeNode root) {
    recursion(root, 0);
    return deep;
}

private void recursion(TreeNode root, int level) {
    if (root == null) {
        deep = Math.max(deep, level);
        return;
    }

    recursion(root.left, level + 1);
    recursion(root.right, level + 1);
}
```

6.[111.二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)
```java
（Facebook、字节跳动、谷歌在半年内面试中考过）
1. 四大算法回顾。分治、动规、回溯、贪心，都可以归结到树结构的遍历。
    分治：将原问题的解分解为若干子问题的解，子问题的解又可以继续分解成更小的子问题的解。自底向上的思维。
    动规：可以认为就是分治，只是强调了在分解子问题的过程中，不会重复计算同样的子问题。自底向上的思维。
    回溯：穷举所有决策路径，每走一步都会到达一个子问题，直到该条路径走到了最小子问题，就开始回头走另外的路径。自顶向下的思维。
    贪心：每走一步都会到达一个子问题，然后根据贪心策略做出选择，直到走到了最小子问题，就认为已经求得了原问题的解。
2.四大算法求解的问题类型
    多阶段决策问题（而不只是最优化！具体是求最值、数量、布尔还是具体决策方案只是问题形式不同）。这种问题总可以分解成同构的子问题，可能的解空间就是所有决策路径的集合。
3.四大算法的时间复杂度
    分治和回溯都穷举了可能解空间中的所有路径，复杂度往往是指数级或阶乘级；
    动规在子问题无重叠的情况下枚举了可能解空间中的某几条路径，复杂度也是指数级或阶乘级，但实际效率会高一些；
    贪心则是只选了可能解空间中的一条路径，复杂度往往是线性级或幂级。但是如果问题本身不具有贪心选择性质，得出的答案不一定正确。
4.四大算法的实现方式
    分治/动态规划：一般管递归形式的叫分治，dp table形式的叫动规。实际上不需要这么区分，带记忆化的可以统称为动规。递归函数一般带有返回值，递归入参就是状态变量，对应dp table的维；
    回溯：一般是递归形式，递归函数一般无返回值（对于除了求具体决策方案的其他问题形式，可能带返回值），入参带有已走的路径和状态变量，通过状态变量得出选择列表；
    贪心无固定实现方式，具体问题具体分析。
5.和树结构的渊源
    多阶段决策问题，面临的局面就是状态，做出决策就会导致状态转移。因为子状态可以继续递推分解，就和树一样具有天然的递归性质。
    对应到树中，状态就是节点，状态转移/做出决策就是边，最小的子状态就是叶子，原问题/原状态就是根。

// 1.BFS，迭代
// 2.分治/动态规划/DFS，自底向上/递归
// 3.回溯/DFS，自顶向下/递归
// 4.DFS/后序遍历，迭代，使用变量保存上一次访问的节点
// 5.DFS/后序遍历，迭代，每个节点入栈出栈两次

待解决// 5.DFS/后序遍历，迭代，每个节点入栈出栈两次
public int minDepth(TreeNode root) {
    if (root == null) return 0;
    Deque<TreeNode> stack = new ArrayDeque<>();
    int level = 0, minLevel = Integer.MAX_VALUE;
    stack.addLast(root);
    stack.addLast(root);
    while (!stack.isEmpty()) {
        root = stack.removeLast();
        if (root == stack.peekLast()) {
            level++;
            if (root.right != null) {
                stack.addLast(root.right);
                stack.addLast(root.right);
            }
            if (root.left != null) {
                stack.addLast(root.left);
                stack.addLast(root.left);
            }
        } else {
            if (root.left == null && root.right == null) minLevel = Math.min(minLevel, level);
            level--;
        }
    }
    return minLevel;
}

待解决// 4.DFS/后序遍历，迭代，使用变量保存上一次访问的节点
public int minDepth(TreeNode root) {
    if (root == null) return 0;
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode last = null;
    int level = 0, minLevel = Integer.MAX_VALUE;
    while (root != null || !stack.isEmpty()) {
        while (root != null) {
            stack.addLast(root);
            level++;
            root = root.left;
        }
        TreeNode tmp = stack.peekLast();
        if (tmp.right != null && tmp.right != last) {
            root = tmp.right;
        } else {
            if (tmp.left == null && tmp.right == null) minLevel = Math.min(minLevel, level);
            last = stack.removeLast();
            level--;
        }
    }
    return minLevel;
}

// 3.回溯/DFS，自顶向下/递归
public int minDepth(TreeNode root) {
    return minDepth(root, 1);
}

// depth 已走过的路径
// root 状态变量（dp 数组的维）
private int minDepth(TreeNode root, int depth) {
    // 最小子状态
    if (root == null) { return depth - 1; }
    if (root.left == null && root.right == null) { return depth; }

    // 由状态变量得出选择列表
    // 该层调用返回，相当于回溯，因为上层的 depth 比该层小 1
    if (root.left == null) { return minDepth(root.right, depth + 1); }
    if (root.right == null) { return minDepth(root.left, depth + 1); }

    return Math.min(minDepth(root.left, depth + 1), minDepth(root.right, depth + 1));
}

// 2.分支/动态规划/DFS，自底向上/递归
public int minDepth(TreeNode root) {
    // 初始条件，dp[null] = 0 , dp[叶子] = 1
    if (root == null) { return 0; }
    if (root.left == null && root.right == null) { return 1; }

    // 动态转移方程
    //             / dp[左孩子] + 1，右孩子为 null
    // dp[非叶子] =  dp[右孩子] + 1，左孩子为 null
    //             \ min(dp[左孩子], dp[右孩子]) + 1，左右孩子都不为 null
    if (root.left == null) { return minDepth(root.right) + 1; }
    if (root.right == null) { return minDepth(root.left) + 1; }

    return Math.min(minDepth(root.left), minDepth(root.right)) + 1;
}

// 1.BFS，迭代
public int minDepth(TreeNode root) {
    if (root == null) {
        return 0;
    }

    int level = 0;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while (!queue.isEmpty()) {
        level ++;
        int count = queue.size();
        root = queue.poll();

        while (count > 0) {
            count --;
            if (root.left == null && root.right == null) {
                return level;
            }

            if (root.left != null) {
                queue.offer(root.left);
            }

            if (root.right != null) {
                queue.offer(root.right);
            }
        }
    }

    return level;
}
```
7.[297.二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)
```java
（Facebook、亚马逊在半年内面试常考）
// Encodes a tree to a single string.
public String serialize(TreeNode root) {
    return mySeri(root, new StringBuilder()).toString();
}

private StringBuilder mySeri(TreeNode root, StringBuilder sb) {
    if (root == null) {
        sb.append("None,");
        return sb;
    }

    sb.append(root.val);
    sb.append(",");
    mySeri(root.left, sb);
    mySeri(root.right, sb);

    return sb;
}

// Decodes your encoded data to tree.
public TreeNode deserialize(String data) {
    String[] dataArray = data.split(",");
    List<String> list = new LinkedList<>(Arrays.asList(dataArray));

    return myDeseri(list);
}

private TreeNode myDeseri(List<String> list) {
    if (list.get(0).equals("None")) {
        list.remove(0);
        return null;
    }

    TreeNode root = new TreeNode(Integer.valueOf(list.get(0)));
    list.remove(0);
    root.left = myDeseri(list);
    root.right = myDeseri(list);

    return root;
}
```
8.[236.二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)
```java
（Facebook 在半年内面试常考）
```
9.[105.从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
```java
（字节跳动、亚马逊、微软在半年内面试中考过）
```
10.[77.组合](https://leetcode-cn.com/problems/combinations/)
```java
（微软、亚马逊、谷歌在半年内面试中考过）
List<List<Integer>> res = new ArrayList<>();
public List<List<Integer>> combine(int n, int k) {
    recursion(res, new ArrayList<>(), n, k, 1);

    return res;
}

private void recursion(List<List<Integer>> res, ArrayList<Integer> cur, int n, int k, int start) {
    if (k == 0) {
        res.add(new ArrayList<>(cur));
        return;
    }

    // 从 start~n 中选择 k 个 <==> 从 start~n-k+1 中选择 1 个
    for (int i = start; i <= n - k + 1; i ++) {
        cur.add(i);
        recursion(res, cur, n, k - 1, i + 1);
        cur.remove(cur.size() - 1);
    }
}
```
11.[46.全排列](https://leetcode-cn.com/problems/permutations/)
```java
（字节跳动在半年内面试常考）
```
12.[47.全排列 II](https://leetcode-cn.com/problems/permutations-ii/)
```java
 （亚马逊、字节跳动、Facebook 在半年内面试中考过）
```
13.[22. 括号生成](https://leetcode-cn.com/problems/generate-parentheses/)
```java

```

14
![牛顿迭代法原理](G:/study\geek\newton_iteration_method.png)
[牛顿迭代法代码](http://www.voidcn.com/article/p-eudisdmk-zm.html)


15.[169. 多数元素](https://leetcode-cn.com/problems/majority-element/description/)
```java

```

16.[17.电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)
```java

```

17.[51.N 皇后](https://leetcode-cn.com/problems/n-queens/)
```java

```

18.[102.二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/#/description)
```java

```

19.[455.分发饼干](https://leetcode-cn.com/problems/assign-cookies/description/)
```java

```

20.[122.买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/description/)
```java

```

21.[55.跳跃游戏](https://leetcode-cn.com/problems/jump-game/)
```java

```

22.[69.x 的平方根](https://leetcode-cn.com/problems/sqrtx/)
```java

```

23.[367.有效的完全平方数](https://leetcode-cn.com/problems/valid-perfect-square/)
```java

```