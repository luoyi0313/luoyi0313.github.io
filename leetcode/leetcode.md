## [删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

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

