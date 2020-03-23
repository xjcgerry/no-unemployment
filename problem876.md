# 876. 链表的中间结点
第一次做出来一道简单题，奖励自己一个耳光吧，真是没用。
## 单指针
````cpp
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
    ListNode* middleNode(ListNode* head) {
        ListNode *p = new ListNode(-1);
        ListNode *res = head;
        p->next = head;
        int n = 0;
        while (p->next != NULL) {
            n++;
            p = p->next;  //这一步一开始忘了
        }

        
        if (n % 2 == 1) {
            for (int i = 0; i < n/2; i++)
                res = res->next;
        }
        else {
            for (int i = 0; i < n / 2; i++)
                res = res->next;
        }
        return res;
    }
};
````
## 快慢指针
快指针走两步，慢指针走一步
````cpp
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
    ListNode* middleNode(ListNode* head) {
        ListNode *fast = head;
        ListNode *slow = head;
        while (fast != NULL && fast->next != NULL) {
            fast = fast->next->next;
            slow = slow->next;
        }
        return slow;
    }
};
````
