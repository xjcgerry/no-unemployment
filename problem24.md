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
````
迭代
前→start→end→后
定义tmp作为start的前驱节点

````CPP
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode *pre = new ListNode(0);
        pre->next = head;
        ListNode *tmp = pre;
        while (tmp->next != NULL && tmp->next->next != NULL){
            ListNode *start = tmp->next;
            ListNode *end = tmp->next->next;
            tmp->next = end;
            start->next = end->next;//先把start和后继结点连接上
            end->next = start;
            tmp = start;
        }
        return pre->next;
    }
};
