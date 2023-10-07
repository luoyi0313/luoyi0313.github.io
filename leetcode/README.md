## [删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

### 标准解：双指针

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* removeNthFromEnd(struct ListNode* head, int n){
    struct ListNode newNode = {0, head};
    struct ListNode *first, *second;

    first = second = &newNode;
    for (int i = 0; i <= n; ++i) first = first->next;
    while (first != NULL) {
        first = first->next;
        second = second->next;
    }
    second->next = second->next->next;
    return newNode.next;
}
```



### 普通解

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


// 首先确定n的定义域，n<=0, 1<= n <= len, n > len
// 删除第一个节点和最后一个节点是否需要特殊处理?
// 未想出遍历一遍的最优解，先实现遍历两遍
// 问题：删除的节点需要释放么，next需要赋为NULL么

struct ListNode* removeNthFromEnd(struct ListNode* head, int n){
  int len = 0;
  int target = 0;
  struct ListNode *headtmp = head;

  if (n <= 0) return head;
  while (headtmp != NULL) {
    len++;
    headtmp = headtmp->next;
  }
  
  if (n > len) return head;
  
  headtmp = head;
  target = len - n + 1;
  if (target == 1) {
    head = head->next;
    headtmp->next = NULL;
    return head;
  } else if (target == len) {
    while (headtmp->next->next != NULL) {
      headtmp = headtmp->next;
    }
    headtmp->next = NULL;
    return head;
  } else {
    for (int i = 0; i < target-2; ++i) {
      headtmp = headtmp->next;
    }
    headtmp->next = headtmp->next->next;
    return head;
  }

  return head;
}
```

