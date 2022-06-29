# LeetCodeNoteBook
该仓库是LeetCode刷题的笔记,刷题路线参考[代码随想录](https://programmercarl.com/),题目解析参考LeetCode官方的解题以及代码随想录的解析。

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
  + **==补充:在LeetCode上发现另一个[解题思路](https://leetcode-cn.com/problems/intersection-of-two-linked-lists-lcci/solution/mian-shi-ti-0207-lian-biao-xiang-jiao-sh-b8hn/))==**
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

+ :star: (简单)[28. 实现 strStr() - 力扣（LeetCode）](https://leetcode.cn/problems/implement-strstr/)
  + 经典的KMP算法，理论上了解且熟悉，但是代码实现和写题目手算不太一样，具体代码实现需要反复品味品位。
  + 代码比较简短，但是还是不能硬背，还是要多理解。主要是回退这一步容易搞乱，同时有多种实现方式
  + 自己掌握的话习惯一种实现方式就可以了：记住==得到前缀表之后统一减1==的方法就可以。注意回退的下标。
  + ==不变量==：j永远代表前缀的最后一个字符，i永远代表当前正在比较的主字符串字符，j+1则代表当前正在比较的模板字符串中的字符。
  + ==不变规则==：i表示大字符串中的下标，总是在循环中递增（主字符串不回退）。j的控制(自增或回退)在循环体中在一定条件下操作。

+ (**X**)(简单)[459. 重复的子字符串 - 力扣（LeetCode）](https://leetcode.cn/problems/repeated-substring-pattern/)
  + 利用KMP，保证求出next数组之后最后一个不为-1且 **字符长度**-**Next数组最后一个元素**-**1**可以整除字符串长度即可。具体证明过程看力扣。
  + 具体证明比较复杂，但是利用例子比较容易看出这个规律。


5. 栈和队列

+ (Easy)[232. 用栈实现队列 - 力扣（LeetCode）](https://leetcode.cn/problems/implement-queue-using-stacks/)

  + 核心思想:利用两个栈(输入栈和输出栈)实现队列
  + 在Golang中没有内置栈数据结构，使用切片代替模拟即可

+ (Easy)[225. 用队列实现栈 - 力扣（LeetCode）](https://leetcode.cn/problems/implement-stack-using-queues/)

  + 核心思想:利用一个队列模拟栈的实现，在模拟移除栈头元素时，只需要将队列中的元素依次出队(除了最后一个元素)，重新加入队尾（或者暂时保存最后更新队列即可）

+ (Easy)[1047. 删除字符串中的所有相邻重复项 - 力扣（LeetCode）](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/)

  + 核心思想:类似于"对对碰"或是"祖玛"游戏，利用栈存储前半部分已遍历的字符，此时栈顶元素总是当前已遍历字符的末尾
  + 当遍历到某字符与栈顶元素相同时，即"对对碰"消除了，此时栈顶元素出栈，新的栈顶元素即代表消除掉重复项之后新的末尾元素，其与下一个未遍历元素继续匹配。
  + 最后栈中剩下的字符即消除相邻重复项之后的字符，简单处理之后即可得到目标字符串

+ (Medium)[150. 逆波兰表达式求值 - 力扣（LeetCode）](https://leetcode.cn/problems/evaluate-reverse-polish-notation/)

  + 理论知识比较熟悉了，只是用代码实现了一下。
  + 核心思想:遇到数字入栈，遇到操作符出栈（注意左右操作符和栈更新即可）

+ (Hard)[239. 滑动窗口最大值 - 力扣（LeetCode）](https://leetcode.cn/problems/sliding-window-maximum/)

  + 核心思想: ==单调队列==
  + 使用Golang具体实现的时候可以发现，这些"花里胡哨"的数据结构的实现其实就是选用底层数据结构(一般都是切片)，在其上做封装即可。单调队列只用保证队列中的元素是单调递增或者递减的即可。

+ (Medium)[347. 前 K 个高频元素 - 力扣（LeetCode）](https://leetcode.cn/problems/top-k-frequent-elements/)

  + 核心思想:==优先级队列、小顶堆==

  + Go具体实现:实现了堆容器的接口后使用堆的方法操作小顶堆。需要实现以下接口:

    1. Len() int
    2. Less(i, j int) bool
    3. Swap(i, j int)

    以上是sort中定义的接口的实现

    4. Push(x any)
    5. Pop() any

6. 二叉树

+ (Easy)[144. 二叉树的前序遍历 - 力扣（LeetCode）](https://leetcode.cn/problems/binary-tree-preorder-traversal/)

  + 递归方法:写递归算法注意

    1. **确定递归函数的参数和返回值：** 确定哪些参数是递归的过程中需要处理的，那么就在递归函数里加上这个参数， 并且还要明确每次递归的返回值是什么进而确定递归函数的返回类型。

    2. **确定终止条件：** 写完了递归算法, 运行的时候，经常会遇到栈溢出的错误，就是没写终止条件或者终止条件写的不对，操作系统也是用一个栈的结构来保存每一层递归的信息，如果递归没有终止，操作系统的内存栈必然就会溢出。

    3. **确定单层递归的逻辑：** 确定每一层递归需要处理的信息。在这里也就会重复调用自己来实现递归的过程。

  + 迭代方法:利用栈

  + 具体流程：初始情况根节点在栈中，后续循环条件为栈不为空。每次出栈一个元素，分别入栈右孩子、左孩子

+ (Easy)[145. 二叉树的后序遍历 - 力扣（LeetCode）](https://leetcode.cn/problems/binary-tree-postorder-traversal/)

  + 三个遍历都类似

+ [145. 二叉树的后序遍历 - 力扣（LeetCode）](https://leetcode.cn/problems/binary-tree-postorder-traversal/)

  1. 递归
  2. 普通迭代(此时中序遍历和前、后序遍历处理不同)
  3. 统一处理的迭代法(标记法)

+ **Loading...**

