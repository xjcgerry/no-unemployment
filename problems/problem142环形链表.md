# 142. 环形链表 II
快慢指针，慢指针一次一步，快指针一次两步，首先判断是否存在环。如果存在环，把fast指针放到链表开头，和slow同步移动，一次一步，直到两指针相遇，即为入环的那个点。
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
    ListNode *detectCycle(ListNode *head) {
        ListNode *fast = head, *slow = head;
        while (true) {  //这里不能用fast!=slow作为判断条件，因为一开始fast和slow都指向head节点
            if (fast == NULL || fast->next == NULL) 
                return NULL;
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow)
                break;
        }
        fast = head;
        while (slow != fast) {
            slow = slow->next;
            fast = fast->next;
        }
        return fast;
    }
};
````
