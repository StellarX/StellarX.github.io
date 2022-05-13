---
title: k个一组翻转链表
date: 2022-05-13 16:40:03
abbrlink: 5783bc85
tags: 
    - 链表
    - 递归
    - leetcode
categories:
    - 算法与数据结构
cover: https://images.pexels.com/photos/9989599/pexels-photo-9989599.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500
---


# 题目
- [k个一组翻转链表](https://leetcode.cn/problems/reverse-nodes-in-k-group/)

# 参考题解
- [递归Java](https://leetcode.cn/problems/reverse-nodes-in-k-group/solution/di-gui-java-by-reedfan-2/)

# 递归：Java实现

- 时间复杂度：O(2n) = O(n)
- 空间复杂度：因为递归次数大概是n / k，所以O(n / k)

```java
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || head.next == null) return head;
        ListNode tail = head;
        for (int i = 0; i < k; i++) {
            if (tail == null) return head;
            tail = tail.next;
        }
        ListNode newHead = reverse(head, tail);
        head.next = reverseKGroup(tail, k);
        return newHead;
    }
    private ListNode reverse(ListNode head, ListNode tail) {
        ListNode pre = null;
        ListNode next = null;
        while (head != tail) {
            next = head.next;
            head.next = pre;
            pre = head;
            head = next;
        }
        return pre;
    }
```

