---
title: 删除链表倒数第n个节点
tags:
  - 链表
  - 指针法
  - leetcode
categories:
  - 算法与数据结构
cover: >-
    https://images.pexels.com/photos/958363/pexels-photo-958363.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500
abbrlink: d9dd8d7d
date: 2022-04-12 20:08:42
---

# 题目
- [删除链表的倒数第 n 个结点](https://leetcode-cn.com/problems/SLwz0R/)

# 分析
- 单链表如何找到倒数第n个节点？
- 利用`双指针`，别忘了考虑特殊情况
- 特殊情况其实就是删除头节点

# Java实现
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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode left = head, right = head;
        for(int i = 0; i < n; ++i) right = right.next;
        if(right == null) {//special case: delete head
            head = left.next;
            return head;
        }
        while(right.next != null) {
            left = left.next;
            right = right.next;
        }
        left.next = left.next.next;
        return head;
    }
}
```
