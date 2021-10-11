## 题目地址(707. 设计链表)

https://leetcode-cn.com/problems/design-linked-list/

## 题目描述

```C++
设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：val 和 next。val 是当前节点的值，next 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 prev 以指示链表中的上一个节点。假设链表中的所有节点都是 0-index 的。

在链表类中实现这些功能：

get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。
addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。
addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。
addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。

示例：
MyLinkedList linkedList = new MyLinkedList();
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1,2);   //链表变为1-> 2-> 3
linkedList.get(1);            //返回2
linkedList.deleteAtIndex(1);  //现在链表是1-> 3
linkedList.get(1);            //返回3

提示：

所有val值都在 [1, 1000] 之内。
操作次数将在  [1, 1000] 之内。
请不要使用内置的 LinkedList 库。
```
## 代码

C++ Code:

```c++

class MyLinkedList {
public:
    struct LinkNode {
        int val;
        LinkNode* next;
        LinkNode(int val):val(val),next(nullptr){};  // 构造函数
    };
    MyLinkedList() {
        dummy_node = new LinkNode(0);
        size = 0;
    }
    
    int get(int index) {
        LinkNode* index_node = dummy_node;
        if (index >= size || index < 0) return -1;
        for (int i = index; i >= 0; i--) {  // 遍历一下找到index_node
            index_node = index_node->next;
        }
        return index_node->val;
    }
    
    void addAtHead(int val) {
        LinkNode* add_node = new LinkNode(val);  // 产生一个数值为val的结点
        add_node->next = dummy_node->next;  // 新结点的next为虚拟头结点的next
        dummy_node->next = add_node;  // 新结点放在头结点之后
        size++;
    }
    
    void addAtTail(int val) {
        LinkNode* p_node = dummy_node;  // 用p_node变量指向遍历链表时的结点
        while (p_node->next != nullptr) {
            p_node = p_node->next;
        }  // 如果不是最后一个结点那就继续遍历
        p_node->next = new LinkNode(val);
        size++;
    }
    
    void addAtIndex(int index, int val) {
        LinkNode* index_node = dummy_node;  // index_node表示需要在该结点前插入新结点
        if (index == size) addAtTail(val);
        else if (index > size) return;
        else if (index <= 0) addAtHead(val);
        else {
            for (int i = index; i >= 0; i--) {  // 遍历一下找到index_node
                index_node = index_node->next;
            }
            /* 退出循环时index_node已找到,只需要在index_node前插入结点即可,插入方法采用
            先插入后换值的方法*/
            LinkNode* add_node = new LinkNode(val);  // 产生新结点
            add_node->next = index_node->next;  // 连链表
            index_node->next = add_node;
            int temp = index_node->val;  // 换值
            index_node->val = add_node->val;
            add_node->val = temp;
            size++;
        }
    }
    
    void deleteAtIndex(int index) {
        LinkNode* index_node = dummy_node;  
        // 这里的index_node表示需要删除的结点的前一个结点
        if (index < size && index >= 0) {
            for (int i = index - 1; i >= 0; i--) {  // 遍历一下找到index_node
                index_node = index_node->next;
            }
            LinkNode* delete_node = index_node->next;  // 暂存待删除结点
            index_node->next = index_node->next->next;
            delete(delete_node);
            size--;
        }
    }

private:
    LinkNode* dummy_node;  // 虚拟头结点
    int size;  // 链表长度
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */

```