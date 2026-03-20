---
date: 2026-03-20 20:34:32
tags:
  - 双指针
  - LeetCode
  - 数组
---

# 双指针算法

方法一没有利用数组 nums1 与 nums2 已经被排序的性质。为了利用这一性质，我们可以使用双指针方法。这一方法将两个数组看作队列，每次从两个数组头部取出比较小的数字放到结果中。

我们为两个数组分别设置一个指针 p1 与 p2 来作为队列的头部指针。代码实现如下：

```
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int p1 = 0, p2 = 0;
        int[] sorted = new int[m + n];
        int cur;
        while (p1 < m || p2 < n) {
            if (p1 == m) {
                cur = nums2[p2++];
            } else if (p2 == n) {
                cur = nums1[p1++];
            } else if (nums1[p1] < nums2[p2]) {
                cur = nums1[p1++];
            } else {
                cur = nums2[p2++];
            }
            sorted[p1 + p2 - 1] = cur;
        }
        for (int i = 0; i != m + n; ++i) {
            nums1[i] = sorted[i];
        }
    }
}
```

## 复杂度分析

- **时间复杂度**：O(m + n)
    
    指针移动单调递增，最多移动 m + n 次，因此时间复杂度为 O(m + n)。
    
- **空间复杂度**：O(m + n)
    
    需要建立长度为 m + n 的中间数组 sorted。