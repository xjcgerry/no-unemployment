# 21. 合并两个有序链表
迭代法
````C++
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode *preHead = new ListNode(-1);//哨兵节点
        ListNode *prev = preHead;

        while (l1 != NULL && l2 != NULL)
        {
            if(l1->val <= l2->val)
            {
                prev->next = l1;
                l1 = l1->next;
            }
            else
            {
                prev->next = l2;
                l2 = l2->next;
            }
            prev = prev->next;
        }
        prev->next = l1 == NULL ? l2 : l1;

        return preHead->next;
    }
};
````
在vscode中测试的完整程序
````CPP
#include <iostream>

struct ListNode{
    int val;
    ListNode *next;
    ListNode(int x): val(x), next(NULL) {}
};

class solution{
    public:
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2){
        ListNode *preHead = new ListNode(-1);
        ListNode *prev = preHead;

        while (l1 !=NULL && l2 != NULL){
            if (l1->val <= l2->val){
                prev->next = l1;
                l1 = l1->next;
            }
            else
            {
                prev->next = l2;
                l2 = l2->next;
            }
            prev = prev->next;
        }
        prev->next = l1 == NULL ? l2 : l1;
        return preHead->next;
    }

};

int main()
{
    ListNode *l1 = new ListNode(1);
    l1->next = NULL;
    ListNode *l1_2 = new ListNode(2);
    l1->next = l1_2;
    l1_2->next = NULL;
    ListNode *l1_3 = new ListNode(4);
    l1_2->next = l1_3;
    l1_3->next = NULL;

    ListNode *l2 = new ListNode(1);
    l2->next = NULL;
    ListNode *l2_2 = new ListNode(3);
    l2->next = l2_2;
    l2_2->next = NULL;
    ListNode *l2_3 = new ListNode(4);
    l2_2->next = l2_3;
    l2_3->next = NULL;

    solution s1;
    std::cout << s1.mergeTwoLists(l1,l2) << std::endl;
    system("pause");
    return 0;
}
