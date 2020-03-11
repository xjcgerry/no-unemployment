# 82. 删除排序链表中的重复元素 II
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
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode *fakeHead = new ListNode(0);
        fakeHead->next = head;
        ListNode *pre;
        ListNode *cur = fakeHead;

        while (cur != NULL){
            pre = cur;
            cur = cur->next;
            while (cur != NULL && cur->next != NULL && cur->val == cur->next->val){
                int val = cur->val;//记录下重复的值
                while (cur != NULL && cur->val == val)
                    cur = cur->next;
            }
        }
        return fakeHead;


    }
};
````
