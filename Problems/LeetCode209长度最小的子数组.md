# 题目地址(209. 长度最小的子数组)

https://leetcode-cn.com/problems/minimum-size-subarray-sum/

## 题目描述

```Cpp
给定一个含有 n 个正整数的数组和一个正整数 target 。

找出该数组中满足其和 ≥ target 的长度最小的 连续子数组 [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。

示例 1：

输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。

示例 2：

输入：target = 4, nums = [1,4,4]
输出：1

示例 3：

输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0

提示：

1 <= target <= 109
1 <= nums.length <= 105
1 <= nums[i] <= 105

进阶：

如果你已经实现 O(n) 时间复杂度的解法, 请尝试设计一个 O(n log(n)) 时间复杂度的解法。
```

## MyCode

### 思路

==参考解题学习滑动窗口方法==后完成该算法.

1. 首先判断所给数组中所有元素总和是否小于目标值$target$
   1. 若小于那么表示该数组中无法找到总和大于$target$的子数组,返回-1
   2. 若总和大于$target$则使用滑动窗口算法寻找最短子数组
      1. 若右指针未超过数组上限,则循环
         1. 若左右指针内元素总和小于$target$那么右移右指针.循环直到元素总和大于$target$
         2. 若左右指针内的元素总和大于$target$那么右移左指针并记录子数组长度,若子数组长度小于$res$则更新$res$.循环直到元素总和小于$target$

### 代码

```c++
class Solution {
public:
    int vector_sum(vector<int> vin){
        int res = 0;
        for(int i = 0; i < vin.size(); i++){
            res += vin[i];
        }
        return res;
    }

    int minSubArrayLen(int target, vector<int>& nums) {
        int left = 0, right = 0, res = nums.size() + 1, sum = 0;
        if(vector_sum(nums) < target) return 0;
        while(right < nums.size()){
            while(sum < target && right < nums.size()){  // 滑动窗口内综合小于目标
                sum += nums[right];
                right++;
            }
            while(sum >= target && left >= 0){
                res = (right - left) <= res ? right - left : res;
                sum -= nums[left];
                left++;
            }
        }
        return res;
    }
};
```

### 复杂度分析

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$



## BetterCode

### 思路

接下来就开始介绍数组操作中另一个重要的方法：**滑动窗口**。

所谓滑动窗口，**就是不断的调节子序列的起始位置和终止位置，从而得出我们要想的结果**。

这里还是以题目中的示例来举例，s=7， 数组是 2，3，1，2，4，3，来看一下查找的过程：

![209.长度最小的子数组](LeetCode209长度最小的子数组.assets/209.长度最小的子数组.gif)

最后找到 4，3 是最短距离。

其实从动画中可以发现滑动窗口也可以理解为**双指针法**的一种！只不过这种解法更像是一个窗口的移动，所以叫做滑动窗口更适合一些。

在本题中实现滑动窗口，主要确定如下三点：

- 窗口内是什么？
- 如何移动窗口的起始位置？
- 如何移动窗口的结束位置？

窗口就是 满足其和 ≥ s 的长度最小的 连续 子数组。

窗口的起始位置如何移动：如果当前窗口的值大于s了，窗口就要向前移动了（也就是该缩小了）。

窗口的结束位置如何移动：窗口的结束位置就是遍历数组的指针，窗口的起始位置设置为数组的起始位置就可以了。

解题的关键在于 窗口的起始位置如何移动，如图所示：

![leetcode_209](LeetCode209长度最小的子数组.assets/20210312160441942.png)

可以发现**滑动窗口的精妙之处在于根据当前子序列和大小的情况，不断调节子序列的起始位置。从而将O(n^2)的暴力解法降为O(n)。**

### 代码

```cpp
class Solution {
public:
    int minSubArrayLen(int s, vector<int>& nums) {
        int result = INT32_MAX;
        int sum = 0; // 滑动窗口数值之和
        int i = 0; // 滑动窗口起始位置
        int subLength = 0; // 滑动窗口的长度
        for (int j = 0; j < nums.size(); j++) {
            sum += nums[j];
            // 注意这里使用while，每次更新 i（起始位置），并不断比较子序列是否符合条件
            while (sum >= s) {
                subLength = (j - i + 1); // 取子序列的长度
                result = result < subLength ? result : subLength;
                sum -= nums[i++]; // 这里体现出滑动窗口的精髓之处，不断变更i（子序列的起始位置）
            }
        }
        // 如果result没有被赋值的话，就返回0，说明没有符合条件的子序列
        return result == INT32_MAX ? 0 : result;
    }
};
```

### 复杂度分析

时间复杂度：$O(n)$
空间复杂度：$O(1)$

**一些录友会疑惑为什么时间复杂度是O(n)**。

不要以为for里放一个while就以为是$O(n^2)$啊， 主要是看每一个元素被操作的次数，每个元素在滑动窗后进来操作一次，出去操作一次，每个元素都是被被操作两次，所以时间复杂度是2 * n 也就是$O(n)$。