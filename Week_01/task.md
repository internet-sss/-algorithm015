1. 用 add first 或 add last 这套新的 API 改写成 Deque 的代码
```java

```

2.分析 Queue 和 Priority Queue 的源码
```java

```
3.删除排序数组中的重复项（Facebook、字节跳动、微软在半年内面试中考过）
```java
// 1.快排思想，利用指针将不重复的放在指针位置及以前
public int removeDuplicates(int[] nums) {
    if (num.length < 2) {
        return nums.length;
    }
    
    int index = 0;
    for (int i = 1; i < nums.length; i ++) {
        if (nums[i] != nums[i - 1]) {
            nums[++ index] = nums[i];
        }
    }

    return index + 1;
}
```
4.旋转数组（微软、亚马逊、PayPal 在半年内面试中考过）
```java
// 1. 暴力
// 2. 额外数组
// 3. 数组整体反转，0~k-1 反转，k~n-1 反转
// 4. 环状替换

// 3. 数组整体反转，0~k-1 反转，k~n-1 反转
public void rotate(int[] nums, int k) {
    k %= nums.length;
    reverse(nums, 0, nums.length - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, nums.length - 1);
}
public static void reverse(int[] arr, int l, int r) {
    int tmp = 0;
    while (l < r) {
        tmp = nums[l];
        nums[l] = nums[r];
        nums[r] = tmp;
        l ++;
        r --;
    }
}

// 2. 额外数组
public void rotate(int[] nums, int k) {
    int[] arr = new int[nums.length];
    for (int i = 0; i < nums.length; i ++) {
        arr[(i + k) % nums.length] = nums[i];
    }
    for (int i = 0; i < nums.length; i ++) {
        nums[i] = arr[i];
    }
}

// 1.暴力
public void rotate(int[] nums, int k) {
    int tmp = 0;
    for (int i = 0; i < k; i ++) {
        for (int j = 0; j < nums.length; j ++) {
            tmp = nums[nums.length - 1];
            nums[nums.length - 1] = nums[j];
            nums[j] = tmp;
        }
    }
}

```
5.合并两个有序链表（亚马逊、字节跳动在半年内面试常考）
```java
// 1. 双虚拟链表存储
// 2. 递归

// 2.递归
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    if (l1 == null) {
        return l2;
    } else if (l2 == null) {
        return l1;
    } else if (l1.val < l2.val) {
        l1.next = mergeTwoLists(l1.next, l2);
        return l1;
    } else {
        l2.next = mergeTwoLists(l1, l2.next);
        return l2;
    }
}

// 1. 双虚拟链表存储
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode res = new ListNode(-1);
    ListNode pre = res;

    while (l1 != null && l2 != null) {
        if (l1.val < l2.val) {
            // 创建新的节点
            pre.next = new ListNode(l1.val);
            l1 = l1.next;
                
            // // 本地修改
            // pre.next = l1;
            // l1 = l1.next;
            // pre.next.next = null;
        } else {
            pre.next = l2;
            l2 = l2.next;
            pre.next.next = null;
        }
        pre = pre.next;
    }

    if (l1 != null) {
        pre.next = l1;
    }

    if (l2 != null) {
        pre.next = l2;
    }

    return res.next;
}

```
6.合并两个有序数组（Facebook 在半年内面试常考）
```java
// 2. 原地排序
public void merge(int[] nums1, int m, int[] nums2, int n) {
    int p1 = m;
    int p2 = n;
    int p = m + n - 1;

    while (p1 >= 0 && p2 >= 0) {
        nums1[p --] = nums1[p1] > nums2[p2] ? nums1[p1 --] : nums2[p2 --];
    }
    
    // 如果是 nums1 剩余元素，则不用排序
    // 如果是 nums2 剩余元素，则一定是最小的那几个元素
    for (int i = 0; i <= p2; i ++) {
        nums1[i] = nums2[i];
    }
}

// 1. 创建额外空间
public void merge(int[] nums1, int m, int[] nums2, int n) {
    int i = 0;
    int j = 0;
    int index = 0;
    int[] arr = new int[nums1.length];
    while (i < m && j < n) {
        if (nums1[i] < nums2[j]) {
            arr[index ++] = nums1[i ++];
        } else {
            arr[index ++] = nums2[j ++];
        }
    }

    while (i < m) {
        arr[index ++] = nums1[i ++];
    }

    while (j < m) {
        arr[index ++] = nums2[j ++];
    }

    for (int i = 0; i < nums1.length; i ++) {
        nums1[i] = arr[i];
    }

}

```
7.两数之和（亚马逊、字节跳动、谷歌、Facebook、苹果、微软在半年内面试中高频常考）
```java
// 1. 暴力
// 2. 空间换时间，两遍 Hash
// 3. 一遍 Hash

// 3. 一遍 Hash
public int[] twoSum(int[] nums, int target) {
    HashMap<Integer, Integer> memoryMap = new HashMap<>();
    for (int i = 0; i < nums.length; i ++ ) {
        if (memoryMap.containsKey(nums[i])) {
            return new int[] { memoryMap.get(nums[i]), i };
        } else {
            memoryMap.put(target - nums[i], i);
        }
    }

    return new int[] {};
}


// 2.两边 Hash
public int[] twoSum(int[] nums, int target) {
    HashMap<Integer, Integer> memoryMap = new HashMap<>();

    for (int i = 0; i < nums.length; i ++) {
        memoryMap.put(target - nums[i], i);
    }

    for (int i = 0; i < nums.length; i ++) {
        if (memoryMap.containsKey(nums[i]) && memoryMap.get(nums[i]) != i) {
            return new int[] { memoryMap.get(nums[i]), i };
        }
    }

    return new int[] {};
}

// 1. 暴力
public int[] twoSum(int[] nums, int target) {
    if (nums.length < 2) {
        return new int[] {};
    }

    for (int i = 0; i < nums.length - 1; i ++) {
        for (int j = i = 1; j < nums.length; j ++) {
            if (nums[i] + nums[j] == target) {
                return new int[] { i, j };
            }
        }
    }

    return new int[] {};
}
```
8.移动零（Facebook、亚马逊、苹果在半年内面试中考过）
```java
// 1. 额外空间
// 2. 荷兰国旗思想，指针划分区域

// 1. 荷兰国旗思想，指针划分区域
public void moveZeroes(int[] nums) {
    if (nums.length < 2) {
        return ;
    }

    int p = 0;
    
    for (int i = 0; i < nums.length; i ++) {
        if (nums[i] != 0) {
            nums[p ++] = nums[i];
            nums[i] = 0;
        }
    }
}

// 1. 额外空间
public void moveZeroes(int[] nums) {
    int[] arr = new int[nums.length];

    int index = 0;

    for (int i = 0; i < nums.length; i ++) {
        if (nums[i] != 0) {
            arr[index ++] = nums[i];
        }
    }

    for (int i = 0; i < nums.length; i ++) {
        nums[i] = arr[i];
    }
}

```
9.加一（谷歌、字节跳动、Facebook 在半年内面试中考过）
```java
 // 1. 倒序相加，若能走出循环，定有进位
public int[] plusOne(int[] digits) {
    for (int i = digits.length - 1; i >= 0; i --) {
        digits[i] ++;
        digits[i] %= 10;
        if (digits[i] != 0) {
            return digits;
        }
    }

    int[] arr = new int[digits.length + 1];
    arr[0] = 1;
    for (int i = 1; i < arr.length; i ++) {
        arr[i] = digits[i - 1];
    }

    return arr;
}
```

10.设计循环双端队列（Facebook 在 1 年内面试中考过）
```java
class MyCircularDeque {

    private int front;
    private int rear;
    private int capacity;
    private int[] data;
    

    public MyCircularDeque(int k) {
        this.front = 0;
        this.rear = 0;
        this.capacity = k + 1;
        this.data = new int[this.capacity];
        
    }


    public boolean insertFront(int value) {
        if (isFull()) {
            return false;
        }

        front = (front - 1 + capacity) % capacity;
        data[front] = value;

        return true;
    }

    public boolean insertLast(int value){
        if (isFull()) {
            return false;
        }

        data[tail] = value;
        rear = (rear + 1) % capacity;

        return true;
    }

    public boolean deleteFront() {
        if (isEmpty()) {
            return false;
        }

        front = (front + 1) % capacity;

        return true;
    }

    public boolean deleteLast() {
        if (isEmpty()) {
            return false;
        }

        rear = (rear - 1 + capacity) % capacity;

        return true;
    }

    public int getFront() {
        if (isEmpty()) {
            return -1;
        }

        return data[front];
    }

    public int getRear() {
        if (isEmpty()) {
            return -1;
        }

        return data[(rear - 1 + capacity) % capacity];
    }

    public boolean isEmpty() {
        return front == rear;
    }

    public boolean isFull() {
        return (rear + 1) % capacity == front;
    }
}
```

11.接雨水（亚马逊、字节跳动、高盛集团、Facebook 在半年内面试常考）
```java
// 1. 暴力
// 2. 动态规划
// 3. 韦恩图
// 4. 栈

// 4. 栈
public int trap(int[] height) {
    Stack<Integer> stack = new Stack<>();
    int current = 0;
    int res = 0;

    while (current < height.length) {
        // 寻找右侧较高的柱子
        while (!stack.isEmpty() && height[current] > height[stack.peek()]) {
            int h = height[stack.peek()];
            stack.pop();
            // 寻找左边是否有柱子
            if (stack.isEmpty()) {
                break;
            }

            int distance = current - stack.peek() - 1;
            int min = Math.min(height[current], height[stack.peek()]);
            res += distance * (min - h);
        }

        stack.put(current);
        current ++;
    }
}




// 3. 韦恩图
public int trap(int[] height) {
    int maxL = 0;
    int maxR = 0;
    int res = 0;
    int pillar = 0;

    for (int i = 0; i < height.length; i ++) {
        if (maxL < height[i]) {
            maxL = height[i];
        }

        if (maxR < height[height.length - i - 1]) {
            maxR = height[height.length - i - 1];
        }

        pillar += height[i];
        res += maxL + maxR;
    }

    return res - pillar - maxL * height.length;
}

// 2. 动态规划
public int trap(int[] height) {
    int[] maxL = new int[height.length];
    int[] maxR = new int[height.length];
    int res = 0;

    for (int i = 1; i < height.length; i ++) {
        maxL[i] = Math.max(maxL[i - 1], height[i - 1]);
    }

    for (int i = height.length - 2; i >= 0; i --) {
        maxR[i] = Math.max(maxR[i + 1], height[i + 1]);
    }

    int tmp = 0;

    for (int i = 1; i < height.length - 1; i ++) {
        tmp = Math.min(maxL[i], maxR[i]);
        if (tmp > height[i]) {
            res += tmp - height[i];
        }
    }

    return res;
}

// 1. 暴力
public int trap(int[] height) {
    int maxL;
    int maxR;
    int res = 0;

    for (int i = 0; i < height.length; i ++) {
        maxL = 0;
        maxR = 0;
        for (int j = i; j >= 0; j --) {
            maxL = Math.max(maxL, height[j]);
        }

        for (int j = i; j < height.length; j ++) {
            maxR = Math.max(maxR, height[j]);
        }

        res += Math.min(maxL, maxR) - height[i];
    }

    return res;
}
```
