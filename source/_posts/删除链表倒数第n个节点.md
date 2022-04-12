---
title: 删除链表倒数第n个节点
tags:
  - 链表
  - 双指针
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
        ListNode front = head, back = head, p = head;
        for(int i = 0; i < n - 1; ++i)
            back = back.next;
        while(back.next != null) {
            back = back.next;
            front = front.next;
        }
        if(front == head) {//special case: delete head node
            head = head.next;
            return head;
        }
        while(p.next != front)
            p = p.next;
        p.next = front.next;
        return head;
    }
}
```
