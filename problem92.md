# 92. 反转链表 II

·······N ——> 1 ——> 2 ——> 3 ——> 4 ——> 5  
dummy·········g·············p·······removed  

removed = p->next;  //先取要操作的那一位  
p->next = p->next->next;  //把这一位所在的链断开  
removed->next = g->next;  //和前面接上  
g->next = removed;  
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
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        ListNode *dummy = new ListNode(0);
        dummy->next = head;

        ListNode *g = dummy;
        ListNode *p = dummy->next;

        for (int i=0; i<m-1; i++){
            g = g->next;
            p = p->next;
        }

        for (int i=0; i < n-m; i++){
            ListNode *removed = p->next;
            p->next = p->next->next;
            removed->next = g->next;
            g->next = removed;
        }
        return dummy->next;
    }
};
````
