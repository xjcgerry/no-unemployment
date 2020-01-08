# 两数之和
## 题目
给出两个非空的链表用来表示两个非负的整数。其中，它们各自的位数是按照逆序的方式存储的，并且它们的每个节点只能存储一位数字。  
如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。  
您可以假设除了数字 0 之外，这两个数都不会以 0 开头。  
**示例：**  
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)  
输出：7 -> 0 -> 8  
原因：342 + 465 = 807  
## 算法
首先从最低有效位，即列表*l1*和*l2*的表头开始相加。如果两个数字的和≥10，就把进位标志carry设置为1，代入下一次迭代，否则carry=0。  
**伪代码如下：**  
* 将当前节点初始化为返回列表的哑结点。
* 将进位标志carry初始化为0。
* 将p和q初始化为列表*l1*和*l2*的头部。
* 遍历列表*l1*和*l2*直至到达它们的尾端。
    + 将x设为节点p的值。如果p已经到达*l1*的末尾，则将p的值设置为0。
    + 将y设为节点q的值。如果q已经到达*l2*的末尾，则将q的值设置为0。
    + 设定sum=x+y+carry
    + 更新进位标志的值，carry=sum/10
    + 创建一个数值为（sum mod 10）的新节点，并将其设置为当前节点的下一个节点，然后将当前节点前进到下一个节点。
    + 同时，将p和q前进到下一个节点。
* 检查carry=1是否成立，如果成立，则向返回列表追加一个含有数字1的新节点。
* 返回哑结点的下一个节点
````java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyHead = new ListNode(0);
        ListNode p = l1, q = l2, curr = dummyHead; //将curr指向了dummyHead的同个地址
        int carry = 0;
        while (p != null || q != null) { //如果p和q都不是尾结点，进入循环
            int x = (p != null) ? p.val : 0; //如果p不是尾结点，那么x=p.val；如果p是尾结点，那么x=0.
            int y = (q != null) ? q.val : 0;
            int sum = carry + x + y;
            carry = sum / 10;
            curr.next = new ListNode(sum % 10);
            curr = curr.next;
            if (p != null) p = p.next;
            if (q != null) q = q.next;
        }
        if (carry > 0) {
            curr.next = new ListNode(carry);
        }
        return dummyHead.next;
    }
}
