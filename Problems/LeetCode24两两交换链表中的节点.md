# **题目地址(24. 两两交换链表中的节点)**

https://leetcode-cn.com/problems/swap-nodes-in-pairs/

## 题目描述

```c++
给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

示例 1：

输入：head = [1,2,3,4]
输出：[2,1,4,3]

示例 2：

输入：head = []
输出：[]

示例 3：

输入：head = [1]
输出：[1]

提示：

链表中节点的数目在范围 [0, 100] 内
0 <= Node.val <= 100

进阶：你能在不修改链表节点值的情况下解决这个问题吗?（也就是说，仅修改节点本身。）
```

## **C++代码**

### **双指针迭代法**

```c++

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {  // 该解决方案使用双指针遍历法解决，初步尝试，非最优解法
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* first_node = head, * first_next_node;
        ListNode* second_node = (head == nullptr) ? nullptr : head->next, * second_next_node;
        ListNode* tail_node = new ListNode(0), * res_node = tail_node;
        /* 使用两个指针分别遍历奇偶节点,初始值分别指向No.0,No.1节点
         * tail_node表示新链表尾结点,x_next_node变量存储两个子链的下一个节点**/
        while (second_node != nullptr && first_node != nullptr) {  // 跳出循环的条件为:后面只有一个结点或者没有节点了
            first_next_node = second_node->next;  // 要么为null要么为地址
            second_next_node = (first_next_node == nullptr) ? nullptr : first_next_node->next;
            // 若first_next_node为null那么second_next_node也应该为null,否则为first_next_node->next 
            // 先将两个节点互换
            tail_node->next = second_node;  // 将第二个结点与已完成部分链表链接
            second_node->next = first_node;  // 交换
            tail_node = first_node;  // 标识已完成部分尾部
            first_node = first_next_node;  // 更新节点数据
            second_node = second_next_node;
        }
        // 跳出循环只用将最后一个结点连出去就可以
        tail_node->next = first_next_node;  // 连接最后一个节点或最后一个节点的next变量归为nullptr
        return res_node->next;  // 范围虚拟节点的下一个节点(实际头结点)
    }
};

```

#### **复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

### **改进迭代算法**

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummyHead = new ListNode(0);
        dummyHead->next = head;
        ListNode* temp = dummyHead;  // 到此为止思路相同
        while (temp->next != nullptr && temp->next->next != nullptr) {  
        		// 这里有可能存在temp->next == null从而导致temp->next->next报错!
        		// 但是为什么答案里这样写?平时写题时这样的操作经常报错!
        		// 我觉得有可能是在判断语句中,语句出错不影响判断结果
        		/*
            	用'(temp->next == nullptr) ? nullptr : temp->next->next;'代替
            	可以避免这种报错(更稳健,而且还能熟悉三元表达式)
        		*/
            ListNode* node1 = temp->next;
            ListNode* node2 = temp->next->next;
            temp->next = node2;
            node1->next = node2->next;
            node2->next = node1;
            temp = node1;
        }
        return dummyHead->next;
    }
};

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/swap-nodes-in-pairs/solution/liang-liang-jiao-huan-lian-biao-zhong-de-jie-di-91/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

### **递归算法**

#### 思路与算法

> 可以通过递归的方式实现两两交换链表中的节点。
>
> 递归的终止条件是链表中没有节点，或者链表中只有一个节点，此时无法进行交换。
>
> 如果链表中至少有两个节点，则在两两交换链表中的节点之后，原始链表的头节点变成新的链表的第二个节点，原始链表的第二个节点变成新的链表的头节点。链表中的其余节点的两两交换可以递归地实现。在对链表中的其余节点递归地两两交换之后，更新节点之间的指针关系，即可完成整个链表的两两交换。
>
> 用 $head$ 表示原始链表的头节点，新的链表的第二个节点，用 $newHead$ 表示新的链表的头节点，原始链表的第二个节点，则原始链表中的其余节点的头节点是$ newHead.next$。令 $head.next = swapPairs(newHead.next)$，表示将其余节点进行两两交换，交换后的新的头节点为 $head$ 的下一个节点。然后令 $newHead.next = head$，即完成了所有节点的交换。最后返回新的链表的头节点 $newHead$。

实际上,==没看懂==在说啥

==换个解释:==

**其中我们应该关心的主要有三点：**

1. ==返回值==

2. ==调用单元做了什么==

3. ==终止条件==

在本题中：

1. 返回值：交换完成的子链表H
2. 调用单元：设需要交换的两个点为 head 和 next，head 连接后面交换完成的子链表，next 连接 head，完成交换
3. 终止条件：head 为空指针或者 next 为空指针，也就是当前无节点或者只有一个节点，无法进行交换

作者：guanpengchn
链接：https://leetcode-cn.com/problems/swap-nodes-in-pairs/solution/hua-jie-suan-fa-24-liang-liang-jiao-huan-lian-biao/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (head == nullptr || head->next == nullptr) {
            return head;
        }
        ListNode* newHead = head->next;
        head->next = swapPairs(newHead->next);
        newHead->next = head;
        return newHead;
    }
};

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/swap-nodes-in-pairs/solution/liang-liang-jiao-huan-lian-biao-zhong-de-jie-di-91/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

