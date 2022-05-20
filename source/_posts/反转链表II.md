---
title: 反转链表II
tags:
  - 链表
  - 指针法
  - 辅助法
  - leetcode
categories:
  - 算法与数据结构
abbrlink: b17609ee
date: 2022-05-17 23:08:51
---

# 题目

- [反转链表II](https://leetcode.cn/problems/reverse-linked-list-ii/)

# 解析

- 用迭代不烧脑而且快，用递归烧脑而且占空间
- 建一个辅助头节点dummy，可以让代码更简洁且方便

# 迭代法

## Java实现

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        ListNode dummy = new ListNode(0, head);
        ListNode pre = dummy, curr, rear;
        for(int i = 1; i < left; ++i)
            pre = pre.next;
        head = pre;
        pre = pre.next;
        curr = pre.next;
        for(int i = left; i < right; ++i){
            rear = curr.next;
            curr.next = pre;
            pre = curr;
            curr = rear;
        }
        head.next.next = curr;
        head.next = pre; 
        return dummy.next;
    }
}
```

