
## 题目地址(203. 移除链表元素)

https://leetcode-cn.com/problems/remove-linked-list-elements/

## 题目描述

```c++
给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回 新的头节点 。

示例 1：

输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5]

示例 2：

输入：head = [], val = 1
输出：[]

示例 3：

输入：head = [7,7,7,7], val = 7
输出：[]

提示：

列表中的节点数目在范围 [0, 104] 内
1 <= Node.val <= 50
0 <= val <= 50
```

## 代码

### 迭代
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
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* node_p = head, * node_head = nullptr, * node_last = nullptr, * node_delete = nullptr;
        while (node_p != nullptr) {
            if (node_p->val != val) {
                if (node_head == nullptr) {
                    node_head = node_p;
                }
                node_last = node_p;
                node_p = node_p->next;
            }
            else {
                if (node_last == nullptr) {
                    node_delete = node_p;
                    node_p = node_p->next;
                    delete node_delete;
                }
                else {
                    node_last->next = node_p->next;
                    node_delete = node_p;
                    node_p = node_p->next;
                    delete node_delete;
                }
            }
        }
    return node_head;
    }
};
```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

#### 更优代码

也可以用迭代的方法删除链表中所有节点值等于特定值的节点。

用  $temp$ 表示当前节点。如果  $temp$  的下一个节点不为空且下一个节点的节点值等于给定的 $val$ ，则需要删除下一个节点。删除下一个节点可以通过以下做法实现：

$$temp.next = temp.next.next$$

如果 $temp$ 的下一个节点的节点值不等于给定的 $val$，则保留下一个节点，将 $temp$ 移动到下一个节点即可。

当 $temp$ 的下一个节点为空时，链表遍历结束，此时所有节点值等于 $val$ 的节点都被删除。

具体实现方面，由于链表的头节点 $head$ 有可能需要被删除，因此创建哑节点 $dummyHead$，令$ \textit{head}dummyHead.next=head$，初始化 $\textit{temp}=\textit{dummyHead}$，然后遍历链表进行删除操作。最终返回 $\textit{dummyHead}.\textit{next}$ 即为删除操作后的头节点。


```c++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        struct ListNode* dummyHead = new ListNode(0, head);
        struct ListNode* temp = dummyHead;
        while (temp->next != NULL) {
            if (temp->next->val == val) {
                temp->next = temp->next->next;
            } else {
                temp = temp->next;
            }
        }
        return dummyHead->next;
    }
};
```
### 递归

```c++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        if (head == nullptr) {
            return head;
        }
        head->next = removeElements(head->next, val);
        return head->val == val ? head->next : head;
    }
};
```

