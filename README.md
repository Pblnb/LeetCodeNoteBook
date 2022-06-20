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
  + **(==X==)** 题目进阶:要求算法原地运行
    + [解题思路]([环形链表 II（双指针法，清晰图解） - 环形链表 II - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/linked-list-cycle-ii/solution/linked-list-cycle-ii-kuai-man-zhi-zhen-shuang-zhi-/))
    + 思路虽好,但是需要数学运算,真实情况下比较麻烦,借鉴思路即可,该解题思路内总结的也比较好,总结了适用双指针(快慢指针)的几种题型

3. 哈希表

+ (简单)[242. 有效的字母异位词 - 力扣（LeetCode）](https://leetcode.cn/problems/valid-anagram/)
  + 比较容易,解法朴素
+ (简单)[349. 两个数组的交集 - 力扣（LeetCode）](https://leetcode.cn/problems/intersection-of-two-arrays/)
  + 也比较简单,代码随想录中总结了集合、数组的优缺点和适用情况
  + **我使用的是数组解决,但是感觉不是好方案,Go中感觉使用映射(map)比较合适**,因此重新写了一个map的版本
+ (简单)[202. 快乐数 - 力扣（LeetCode）](https://leetcode.cn/problems/happy-number/)
  + 比较简单,思路自然,可能的难点在于**取每位的数字**这个循环
+ (简单)[1. 两数之和 - 力扣（LeetCode）](https://leetcode.cn/problems/two-sum/)
  + 经典两数之和,暴力方法狗都想得到,在此之前做过因此很自然的想到了哈希表的方法,写的也很顺利,应该没问题了
+ (中等)[454. 四数相加 II - 力扣（LeetCode）](https://leetcode.cn/problems/4sum-ii/)
  + 自己做的时候考虑到如果不止四个数组的情况下,比如六个数组,就所有数组掐头去尾,取出中间数组的集合一次遍历,依次更新map.后来发现和答案(代码随想录)中的实现方式相比,在本题中多了不少的循环次数,运行时间也明显慢于答案的方法.
  + 分析自己的方法和答案的方法的时间复杂度:
    + My Solution:**极端情况下根本没有时间上的优化**.中间过程中map的长度依旧会指数增长,极端情况下和暴力解法时间复杂度相同.
    + 代码随想录 Solution:数组数量变多时,最直观的改法:六个数组三三分为两组,O(n\^3)的时间复杂度.使用分治法时似乎最坏情况下时间复杂度依旧是O(n\^3)
+ (简单)[383. 赎金信 - 力扣（LeetCode）](https://leetcode.cn/problems/ransom-note/)
  + 简单,和#242 有效的字母异位词 基本上相差不大
+ (中等)[15. 三数之和 - 力扣（LeetCode）](https://leetcode.cn/problems/3sum/)
  + 在哈希表章节里，但是并不适合用哈希表解决(要求不重复,故需要大量去重操作)，更适合使用双指针。
  + **可以再看看，注意对比同类题型(题型相同但方法不同)**

+ (中等)[18. 四数之和 - 力扣（LeetCode）](https://leetcode.cn/problems/4sum/)
  + 想复杂了，没想到只是加了一层循环。此类问题往后延伸也都是加一层循环，注意与[454. 四数相加 II - 力扣（LeetCode）](https://leetcode.cn/problems/4sum-ii/)区分


4. 字符串

+ (简单)[344. 反转字符串 - 力扣（LeetCode）](https://leetcode.cn/problems/reverse-string/)
  + 简单。
+ (简单)[541. 反转字符串 II - 力扣（LeetCode）](https://leetcode.cn/problems/reverse-string-ii/)
  + 比较简单，模拟过程中注意边界即可。
+ (简单)[剑指 Offer 05. 替换空格 - 力扣（LeetCode）](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)
  + 比较简单，纠结了半天怎么原地运行，不带来任何额外的空间开销，但是由于Go语法中区分string和[]byte，因此只能创建一个变量用于接收切片。如果硬要只用string不用[]byte的话反而会很麻烦，得不偿失。
+ **==X==**(中等)[151. 颠倒字符串中的单词 - 力扣（LeetCode）](https://leetcode.cn/problems/reverse-words-in-a-string/)
  + 这题是上面三道题的综合，第一次做的时候想不出来原地的方法...

+ (简单)[剑指 Offer 58 - II. 左旋转字符串 - 力扣（LeetCode）](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)
  + 有了上面的基础就很简单了，在链表中也有类似题，思路一样，都是利用反转（由此可见反转的重要性）

+ **Loading...**

