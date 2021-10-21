# 题目地址(977. 有序数组的平方)

https://leetcode-cn.com/problems/squares-of-a-sorted-array/

## 题目描述

```c++
给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。

示例 1：

输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]

示例 2：

输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]

提示：

1 <= nums.length <= 104
-104 <= nums[i] <= 104
nums 已按 非递减顺序 排序

进阶：

请你设计时间复杂度为 O(n) 的算法解决本问题
```

##  MyCode

### 思路

1. 判断原始数组中是否有正有负
   1. 若数组头元素小于0,尾元素大于0,则说明数组有正有负
   2. 若数组头尾元素都大于0,则数组只有正数
   3. 若数组头尾元素都小于0,则数组只有负数
2. 根据数组类型使用对应方法处理数组,生成有序平方数组
   1. 有正有负的数组需要通过遍历找到正负数分隔点后设置两个指针分别往前往后遍历
   2. 只有正数的数组从头到尾遍历即可
   3. 只有负数的数组从尾到头遍历即可

### **代码**

```c++
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        vector<int> ansVec(nums.size());
        int i, j, positive, i_squ, j_squ, pos = 0;
      	// 使用i遍历负数，使用j遍历正数
        if(nums.front() < 0 && nums.back() >= 0){
        // 若数组有正有负则需要判断正负分界点
            for(positive = 0; positive < nums.size(); positive++) {
                if(nums[positive] >= 0) {
                    j = positive;
                    i = positive - 1;
                    break;
                }
            }
            while(i >= 0 && j < nums.size()) {
            // 若i和j都在遍历范围内
                i_squ = pow(nums[i], 2);
                j_squ = pow(nums[j], 2);
                if(i_squ <= j_squ) {
                    ansVec[pos] = i_squ;
                    i--;
                }
                else {
                    ansVec[pos] = j_squ;
                    j++;
                }
                pos++;
            }
            while(i < 0 && j < nums.size()) {
            // 若所有负数遍历完毕，正数仍有剩余
                j_squ = pow(nums[j], 2);
                ansVec[pos] = j_squ;
                j++;
                pos++;
            }
            while(i >= 0 && j >= nums.size()) {
            // 若所有正数遍历完毕，负数仍有剩余
                i_squ = pow(nums[i], 2);
                ansVec[pos] = i_squ;
                i--;
                pos++;
            }
        }
        else if(nums.front() >= 0 && nums.back() >= 0){
        // 若数组只有正数直接正向依次填入就好
            j = 0;
            while(j < nums.size()) {
                ansVec[j] = pow(nums[j], 2);
                j++;
            }
        }
        else if(nums.front() < 0 && nums.back() < 0){
        // 若数组只有负数直接逆向依次填入就好
            i = nums.size() - 1;
            pos = 0;
            while(i >= 0) {
                ansVec[pos] = pow(nums[i], 2);
                i--;
                pos++;
            }
        }
        return ansVec;
    }
};
```

### **复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

### **反思**

不是暴力求解，思路自然易于理解。但是对于算法题来说,该解法代码过于==冗长==。



## BetterCode:双指针法

### 思路

数组其实是有序的， 只不过负数平方之后可能成为最大数了。

那么数组平方的**最大值**就在数组的两端，不是**最左边**就是**最右边**，不可能是中间。

此时可以考虑双指针法了，$i$指向起始位置，$j$指向终止位置。

定义一个新数组$result$，和A数组一样的大小，让$k$指向$result$数组终止位置。

如果`A[i] * A[i] < A[j] * A[j]`那么`result[k--] = A[j] * A[j];` 。

如果`A[i] * A[i] >= A[j] * A[j]` 那么`result[k--] = A[i] * A[i];` 。

如动画所示：

![img](LeetCode977有序数组的平方.assets/977.有序数组的平方.gif)

### 代码

```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& A) {
        int k = A.size() - 1;
        vector<int> result(A.size(), 0);
        for (int i = 0, j = A.size() - 1; i <= j;) { // 注意这里要i <= j，因为最后要处理两个元素
            if (A[i] * A[i] < A[j] * A[j])  {
                result[k--] = A[j] * A[j];
                j--;
            }
            else {
                result[k--] = A[i] * A[i];
                i++;
            }
        }
        return result;
    }
};
```

### 复杂度分析

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$