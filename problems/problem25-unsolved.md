# 25. K 个一组翻转链表
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
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode *cur = head;
        int count = 0;
        while (cur != NULL && count != k){
            cur = cur->next;
            count++;
        }
        //此时cur是一组节点的下一个节点，也就是一组节点的头结点
        if (count == k){
            //递归的时候，每次调用此函数，都将整个链表分为【前k个待翻转节点】和【余下链表】
            //然后先把第一部分进行翻转，对余下的部分进行操作。
            cur = reverseKGroup(cur, k);
            while (count != 0){
                count--;
                ListNode *tmp = head->next;
                head->next = cur;
                cur = head;
                head = tmp;
            }
            head = cur;
        }
        return head;
    }
};
````
