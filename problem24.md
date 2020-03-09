# 24. 两两交换链表中的节点
递归
````CPP
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (head == NULL || head->next == NULL)
            return head;
        ListNode *next = head->next;
        head->next = swapPairs(next->next);//把head和next的后继结点连接
        next->next = head;
        return next;
    }
};
