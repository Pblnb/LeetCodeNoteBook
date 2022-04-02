# 题目地址(206. 反转链表)

https://leetcode-cn.com/problems/reverse-linked-list/

## 题目描述

```c++
给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。

示例 1：

输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]

示例 2：

输入：head = [1,2]
输出：[2,1]

示例 3：

输入：head = []
输出：[]

提示：

链表中节点的数目范围是 [0, 5000]
-5000 <= Node.val <= 5000

进阶：链表可以选用迭代或递归方式完成反转。你能否用两种方法解决这道题？
```

## 代码

- 语言支持：C++

C++ Code:

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
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head == nullptr) return nullptr;
        ListNode* p_node = head->next, * last_node = head, * next_node;
        // 使用p_node代表遍历中的结点,last_node代表上一个结点
        while (p_node != nullptr) {
            next_node = p_node->next;
            // 由于要改变p_node的next变量,会导致链表断链,因此使用一个变量存储下一个结点
            p_node->next = last_node;  // 使该结点指向前一个结点
            last_node = p_node;
            p_node = next_node;
        }
        //跳出循环时,p_node为空,last_node指向原链表最后一个结点
        head->next = nullptr;  // 原链表第一个结点现在是最后一个结点，因此将next域设为空指针
        return last_node;
    }
};

```

**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

## 思路

如果再定义一个新的链表，实现链表元素的反转，其实这是对内存空间的浪费。

其实只需要改变链表的next指针的指向，直接将链表反转 ，而不用重新定义一个新的链表，如图所示:

![206_反转链表](./LeetCode206反转链表.assets/20210218090901207.png)

之前链表的头节点是元素1， 反转之后头结点就是元素5 ，这里并没有添加或者删除节点，仅仅是改表next指针的方向。

那么接下来看一看是如何反转呢？

我们拿有示例中的链表来举例，如动画所示：

![img](./LeetCode206反转链表.assets/008eGmZEly1gnrf1oboupg30gy0c44qp.gif)

首先定义一个cur指针，指向头结点，再定义一个pre指针，初始化为null。

然后就要开始反转了，首先要把 cur->next 节点用tmp指针保存一下，也就是保存一下这个节点。

为什么要保存一下这个节点呢，因为接下来要改变 cur->next 的指向了，将cur->next 指向pre ，此时已经反转了第一个节点了。

接下来，就是循环走如下代码逻辑了，继续移动pre和cur指针。

最后，cur 指针已经指向了null，循环结束，链表也反转完毕了。 此时我们return pre指针就可以了，pre指针就指向了新的头结点。