# LeetCodeNoteBook
该仓库是LeetCode刷题的笔记,刷题路线参考[代码随想录]([代码随想录 (programmercarl.com)](https://programmercarl.com/)),题目解析参考LeetCode官方的解题以及代码随想录的解析。

**问题标题前的X符号表示第一次不能解决的问题，应该注重复习的题目**

## Menu

**该部分前一小部分使用C++,后面使用Go(笔记中虽没有,但全部题目都使用Go实现过)**

1. 线性表

+ (简单) LeetCode#1 [两数之和](./Problems/LeetCode1两数之和.md)
+ (简单) LeetCode#27 [移除元素](./Problems/LeetCode27移除元素.md)
+ (简单) LeetCode#704 [二分查找](./Problems/LeetCode704二分查找.md)
+ (中等) LeetCode#59 [螺旋矩阵II](./Problems/LeetCode59螺旋矩阵II.md)
+ (简单) LeetCode#977 [有序数组的平方](./Problems/LeetCode977有序数组的平方.md)
+ X (中等) LeetCode#209 [长度最小的子数组](./Problems/LeetCode209长度最小的子数组.md)

2. 链表

+ (简单) LeetCode.#203 [移除链表元素](./Problems/LeetCode203移除链表元素.md)
+ (中等) LeetCode.#707 [设计链表](./Problems/LeetCode707设计链表.md)
+ (简单) LeetCode.#206 [反转链表](./Problems/LeetCode206反转链表.md)
+ (中等) LeetCode.#24 [两两交换链表中的节点](./Problems/LeetCode24两两交换链表中的节点.md)

​	(每题都做笔记太浪费时间了,一下部分会在目录中对做题情况进行简要的描述,用于标记第一次做题情况,包括是否有参考别人的思路,是否需要复习等内容)

+ (中等) LeetCode.#19 删除链表的倒数第N个结点
  + 比较简单,可以想到较好的解题思路
+ (简单) LeetCode.面试题02.07 链表相交
  + 不算太难,但是第一反应的思路和较优思路(指代码随想录)不同,但时间复杂度相同代码也不难写
  + **总结:可以简单回顾回顾**
  + **==补充:在LeetCode上发现另一个[解题思路]([面试题 02.07. 链表相交（双指针，清晰图解） - 链表相交 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/intersection-of-two-linked-lists-lcci/solution/mian-shi-ti-0207-lian-biao-xiang-jiao-sh-b8hn/))==**
    + 该思路比较巧妙,也可以看看
+ (中等) LeetCode.#142 环形链表II
  + 问题不难,容易想到偏暴力的算法,但是需要额外空间开销
  + **(X)** 题目进阶:要求算法原地运行
    + [解题思路]([环形链表 II（双指针法，清晰图解） - 环形链表 II - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/linked-list-cycle-ii/solution/linked-list-cycle-ii-kuai-man-zhi-zhen-shuang-zhi-/))
    + 思路虽好,但是需要数学运算,真实情况下比较麻烦,借鉴思路即可,该解题思路内总结的也比较好,总结了适用双指针(快慢指针)的几种题型

3. 哈希表

+ (简单)[LeetCode.#242 有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/)
  + 比较容易,解法朴素
+ (简单)[LeetCode.#349 两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)
  + 也比较简单,代码随想录中总结了集合、数组的优缺点和适用情况
  + **我使用的是数组解决,但是感觉不是好方案,Go中感觉使用映射(map)比较合适**,因此重新写了一个map的版本
+ (简单)[LeetCode.#202 快乐数](https://leetcode-cn.com/problems/happy-number/)
  + 比较简单,思路自然,可能的难点在于**取每位的数字**这个循环
+ **Loading...**

