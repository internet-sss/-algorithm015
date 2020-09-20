
1.[860. 柠檬水找零](https://leetcode-cn.com/problems/lemonade-change/description/)
```java
public boolean lemonadeChange(int[] bills) {
    int five = 0;
    int ten = 0;

    for (int bill: bills) {
        if (bill == 5) {
            five ++;
        } else if (bill == 10) {
            if (five == 0) {
                return false;
            }
            five --;
            ten ++;
        } else {
            if (five > 0 && ten > 0) {
                five --;
                ten --;
            } else if (five >= 3) {
                five -= 3;
            } else {
                return false;
            }
        }
    }

    return true;
}
```

2.[122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/description/)
```java
public int maxProfit(int[] prices) {
    int sum = 0;
    int index = 0;
    int tmp = 0;

    for (int i = 1; i < prices.length; i ++) {
        tmp = prices[i] - prices[index];
        if (tmp > 0) {
            sum += tmp; 
        } 
        
        index = i;
    }

    return sum;
}
```

3.[455. 分发饼干](https://leetcode-cn.com/problems/assign-cookies/description/)
```java

```

4.[874. 模拟行走机器人](https://leetcode-cn.com/problems/walking-robot-simulation/description/)
```java

```

5.[127. 单词接龙](https://leetcode-cn.com/problems/word-ladder/description/)
```java

```

6.[200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)
```java

```

7.[529. 扫雷游戏](https://leetcode-cn.com/problems/minesweeper/description/)
```java

```

8.[55. 跳跃游戏](https://leetcode-cn.com/problems/jump-game/)
```java

```

9.[33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)
```java


```

10.[74. 搜索二维矩阵](https://leetcode-cn.com/problems/search-a-2d-matrix/)
```java

```

11.[153. 寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)
```java

```

12.[126. 单词接龙 II](https://leetcode-cn.com/problems/word-ladder-ii/description/)
```java

```

13.[45. 跳跃游戏 II](https://leetcode-cn.com/problems/jump-game-ii/)
```java

```

14.[53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)
```java

```

15.[198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/)
```java

```

16.[1143. 最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/)
```java

```

17.[120. 三角形最小路径和](https://leetcode-cn.com/problems/triangle/description/)
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