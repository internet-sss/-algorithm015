学习笔记


1.使用二分查找，寻找一个半有序数组 [4, 5, 6, 7, 0, 1, 2] 中间无序的地方
说明：同学们可以将自己的思路、代码写在第 4 周的学习总结中
```java
存在上下界、单调、通过索引访问
折半查找


有序数组 --> 默认递增 --> 大小关系 左 < 中 < 右

若大小关系发生变化，则靠近答案区域


low = 0;
high = arr.length - 1;
left = arr[low]
right = arr[high];

mid = low + (high - low) >> 1
if (arr[mid] < arr[low]) {
    // 右半部分不要
    high = mid;
} else if (arr[mid] > arr[high]) {
    // 左半部分不要
    low = mid;
} else {
    continue;
}
```