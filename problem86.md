# 86. 分隔链表
把原来的链表分成两部分，定义两个指示节点，以及两个哑结点
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
    ListNode* partition(ListNode* head, int x) {
        //before和after追踪两个链表，before_head和after_head是哑结点
        ListNode *before_head = new ListNode(0);
        ListNode *before = before_head;
        ListNode *after_head = new ListNode(0);
        ListNode *after = after_head;

        while (head != NULL){
            if (head->val < x){
                before->next = head;
                before = before->next;
            } else {
                after->next = head;
                after = after->next;
            }
            head = head->next;
        }
        after->next = NULL;
        before->next = after_head->next;

        return before_head->next;

    }
};
````
