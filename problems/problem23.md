# 23. 合并K个排序链表
调用problem21中的函数
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        int size = lists.size();
        if (size == 0){
            return nullptr;
        }
        if (size == 1){
            return lists[0];
        }
        ListNode *p = lists[0];
        for (int i = 1; i < size; i++){
            p = merge2(p, lists[i]);
        }
        return p;
    }
    ListNode* merge2(ListNode *l1, ListNode *l2){
        ListNode *preHead = new ListNode(-1);
        ListNode *prev = preHead;

        while (l1 != NULL && l2 != NULL){
            if (l1->val <= l2->val){
                prev->next = l1;
                l1 = l1->next;
            }
            else{
                prev->next = l2;
                l2 = l2->next;
            }
            prev = prev->next;
        }
        prev->next = l1 == NULL ? l2:l1;
        return preHead->next;
    }
};
